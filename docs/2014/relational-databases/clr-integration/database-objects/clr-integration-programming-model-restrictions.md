---
title: Restricciones del modelo de programación de integración CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a7b7dfcbd9d7cc7407ed33cc0ea00e93df839b93
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48187945"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restricciones del modelo de programación de la integración CLR
  Cuando se está generando un procedimiento almacenado administrado u otro objeto de base de datos administrado, hay realiza ciertas comprobaciones de código [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] realiza comprobaciones en el ensamblado de código administrado cuando se registra primero en la base de datos mediante el `CREATE ASSEMBLY` instrucción y también en tiempo de ejecución. El código administrado también se comprueba en tiempo de ejecución porque en un ensamblado puede haber rutas de acceso al código que nunca se hayan alcanzado realmente en tiempo de ejecución.  Esto proporciona flexibilidad para registrar ensamblados de terceros, de manera especial, de forma que no se debe bloquear un ensamblado donde haya un código 'no seguro' diseñado para que se ejecute en un entorno cliente pero nunca se ejecutaría en el CLR hospedado. Los requisitos que el código administrado debe cumplir dependen de si el ensamblado se registra como `SAFE`, `EXTERNAL_ACCESS`, o `UNSAFE`, `SAFE` que se va las más estrictas y, a continuación se enumeran.  
  
 Además de las restricciones que se ubican en los ensamblados de código administrado, también hay permisos de seguridad de código que se conceden. Common Language Runtime (CLR) admite un modelo de seguridad denominado seguridad de acceso del código (CAS) para el código administrado. En este modelo, se conceden permisos a los ensamblados basados en la identidad del código. Los ensamblados `SAFE`, `EXTERNAL_ACCESS` y `UNSAFE` tienen permisos de CAS diferentes. Para obtener más información, consulte [CLR Integration Code Access Security](../security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Comprobaciones de CREATE ASSEMBLY  
 Cuando se ejecuta la instrucción `CREATE ASSEMBLY` las comprobaciones siguientes se realizan para cada nivel de seguridad.  Si se produce un error en cualquier comprobación, se producirá un error en `CREATE ASSEMBLY` con un mensaje de error.  
  
### <a name="global-any-security-level"></a>Global (cualquier nivel de seguridad)  
 Todos los ensamblados a los que se hace referencia deben cumplir uno o más de los criterios siguientes:  
  
-   El ensamblado ya está registrado en la base de datos.  
  
-   El ensamblado es uno de los ensamblados compatibles. Para obtener más información, consulte [admite bibliotecas de .NET Framework](supported-net-framework-libraries.md).  
  
-   Usa `CREATE ASSEMBLY FROM`  *\<ubicación >,* y están disponibles en todos los ensamblados que se hace referencia y sus dependencias  *\<ubicación >*.  
  
-   Usa `CREATE ASSEMBLY FROM`  *\<bytes... >,* y todas las referencias se especifican a través de espacio separados por bytes.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Todos los ensamblados `EXTERNAL_ACCESS` deben cumplir los criterios siguientes:  
  
-   Los campos estáticos no se usan para almacenar información. Se permiten los campos estáticos de solo lectura.  
  
-   Se pasa la prueba PEVerify. La herramienta PEVerify (peverify.exe), que comprueba que el código MSIL y los metadatos asociados cumplen los requisitos de seguridad de tipos, se proporciona con .NET Framework SDK.  
  
-   La sincronización, por ejemplo no se usa con la clase `SynchronizationAttribute`.  
  
-   No se usan métodos de finalizador.  
  
 Los atributos personalizados siguientes no se permiten en ensamblados `EXTERNAL_ACCESS`:  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   Se comprueban todas las condiciones del ensamblado `EXTERNAL_ACCESS`.  
  
## <a name="runtime-checks"></a>Comprobaciones en tiempo de ejecución  
 En tiempo de ejecución, el ensamblado de código se comprueba para las condiciones siguientes. Si se encuentra cualquiera de estas condiciones, el código administrado no se puede ejecutar y se iniciará una excepción.  
  
### <a name="unsafe"></a>UNSAFE  
 Cargar un ensamblado, explícitamente llamando al método `System.Reflection.Assembly.Load()` desde una matriz de bytes o implícitamente a través del uso del espacio de nombres `Reflection.Emit`, no se permite.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Se comprueban todas las condiciones `UNSAFE`.  
  
 Todos los tipos y métodos anotados con los siguientes valores de atributo de protección de host (HPA) en la lista compatible de ensamblados no están admitidos.  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Synchronization  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 Para obtener más información acerca de los HPA y una lista de tipos no permitidos y los miembros de los ensamblados compatibles, consulte [atributos de protección de Host y programación de integración de CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Se comprueban todas las condiciones `EXTERNAL_ACCESS`.  
  
## <a name="see-also"></a>Vea también  
 [Bibliotecas compatibles de .NET Framework](supported-net-framework-libraries.md)   
 [Seguridad de acceso del código de integración de CLR](../security/clr-integration-code-access-security.md)   
 [Atributos de protección de host y programación de la integración CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Crear un ensamblado](../assemblies/creating-an-assembly.md)  
  
  
