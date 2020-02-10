---
title: Restricciones del modelo de programación de la integración CLR | Microsoft Docs
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
ms.openlocfilehash: a9b51e0fc192c94b32b4d496523dbf3c9216efd6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62873819"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restricciones del modelo de programación de la integración CLR
  Al compilar un procedimiento almacenado administrado u otro objeto de base de datos administrado, algunas comprobaciones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] código realizadas por realiza comprobaciones en el ensamblado de código administrado cuando se registra por primera `CREATE ASSEMBLY` vez en la base de datos, mediante la instrucción y también en tiempo de ejecución. El código administrado también se comprueba en tiempo de ejecución porque en un ensamblado puede haber rutas de acceso al código que nunca se hayan alcanzado realmente en tiempo de ejecución.  Esto proporciona flexibilidad para registrar ensamblados de terceros, de manera especial, de forma que no se debe bloquear un ensamblado donde haya un código 'no seguro' diseñado para que se ejecute en un entorno cliente pero nunca se ejecutaría en el CLR hospedado. Los requisitos que debe cumplir el código administrado dependen de si el ensamblado está registrado `SAFE`como `EXTERNAL_ACCESS`, o `UNSAFE`, `SAFE` siendo el más estricto y se enumeran a continuación.  
  
 Además de las restricciones que se ubican en los ensamblados de código administrado, también hay permisos de seguridad de código que se conceden. Common Language Runtime (CLR) admite un modelo de seguridad denominado seguridad de acceso del código (CAS) para el código administrado. En este modelo, se conceden permisos a los ensamblados basados en la identidad del código. Los ensamblados `SAFE`, `EXTERNAL_ACCESS` y `UNSAFE` tienen permisos de CAS diferentes. Para obtener más información, vea [seguridad de acceso del código de integración CLR](../security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Comprobaciones de CREATE ASSEMBLY  
 Cuando se ejecuta la instrucción `CREATE ASSEMBLY` las comprobaciones siguientes se realizan para cada nivel de seguridad.  Si se produce un error en cualquier comprobación, se producirá un error en `CREATE ASSEMBLY` con un mensaje de error.  
  
### <a name="global-any-security-level"></a>Global (cualquier nivel de seguridad)  
 Todos los ensamblados a los que se hace referencia deben cumplir uno o más de los criterios siguientes:  
  
-   El ensamblado ya está registrado en la base de datos.  
  
-   El ensamblado es uno de los ensamblados compatibles. Para obtener más información, consulte [supported .NET Framework Libraries](supported-net-framework-libraries.md).  
  
-   Está usando `CREATE ASSEMBLY FROM` * \<> de ubicación,* y todos los ensamblados a los que se hace referencia y sus dependencias están disponibles en * \<la ubicación>*.  
  
-   Está utilizando `CREATE ASSEMBLY FROM` * \<bytes... >* y todas las referencias se especifican a través de bytes separados por espacios.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
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
 La carga de un ensamblado, ya sea `System.Reflection.Assembly.Load()` explícitamente llamando al método desde una matriz de bytes o implícitamente a través del uso del `Reflection.Emit` espacio de nombres, no se permite.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
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
  
 Para obtener más información sobre hPa y una lista de tipos y miembros no permitidos en los ensamblados admitidos, vea [atributos de protección del host y programación de la integración CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Se comprueban todas las condiciones `EXTERNAL_ACCESS`.  
  
## <a name="see-also"></a>Consulte también  
 [Bibliotecas de .NET Framework compatibles](supported-net-framework-libraries.md)   
 [Seguridad de acceso del código de integración CLR](../security/clr-integration-code-access-security.md)   
 [Atributos de protección del host y programación de la integración CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Crear un ensamblado](../assemblies/creating-an-assembly.md)  
  
  
