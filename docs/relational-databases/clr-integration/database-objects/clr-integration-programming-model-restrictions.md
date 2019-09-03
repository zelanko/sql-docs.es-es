---
title: Restricciones del modelo de programación de la integración CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
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
ms.openlocfilehash: c019b50f896109a699869d748d8eef20b57d6edb
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212370"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restricciones del modelo de programación de la integración CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Al compilar un procedimiento almacenado administrado u otro objeto de base de datos administrado, se deben tener en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuenta ciertas comprobaciones de código. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]realiza comprobaciones en el ensamblado de código administrado cuando se registra por primera vez en la base de datos, mediante la instrucción **Create Assembly** y también en tiempo de ejecución. El código administrado también se comprueba en tiempo de ejecución porque en un ensamblado puede haber rutas de acceso al código que nunca se hayan alcanzado realmente en tiempo de ejecución.  Esto proporciona flexibilidad para registrar ensamblados de terceros, de manera especial, de forma que no se debe bloquear un ensamblado donde haya un código 'no seguro' diseñado para que se ejecute en un entorno cliente pero nunca se ejecutaría en el CLR hospedado. Los requisitos que debe cumplir el código administrado dependen de si el ensamblado está registrado como **Safe**, **external_access**o **Unsafe**, **Safe** es el más estricto y se enumeran a continuación.  
  
 Además de las restricciones que se ubican en los ensamblados de código administrado, también hay permisos de seguridad de código que se conceden. Common Language Runtime (CLR) admite un modelo de seguridad denominado seguridad de acceso del código (CAS) para el código administrado. En este modelo, se conceden permisos a los ensamblados basados en la identidad del código. Los ensamblados **Safe**, **external_access**y Unsafe tienen permisos CAS diferentes. Para obtener más información, vea [seguridad de acceso del código de integración CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Comprobaciones de CREATE ASSEMBLY  
 Cuando se ejecuta la instrucción **Create Assembly** , se realizan las siguientes comprobaciones para cada nivel de seguridad.  Si se produce un error en alguna comprobación, se producirá un error en **Create Assembly** con un mensaje de error.  
  
### <a name="global-any-security-level"></a>Global (cualquier nivel de seguridad)  
 Todos los ensamblados a los que se hace referencia deben cumplir uno o más de los criterios siguientes:  
  
-   El ensamblado ya está registrado en la base de datos.  
  
-   El ensamblado es uno de los ensamblados compatibles. Para obtener más información, consulte [supported .NET Framework Libraries](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
-   Está usando **Create Assembly from** _\<Location >,_ y todos los ensamblados a los que se hace referencia y sus dependencias están disponibles en  *\<la ubicación >* .  
  
-   Está usando **Create Assembly from** _\<bytes... >_ y todas las referencias se especifican a través de bytes separados por espacios.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Todos los ensamblados **external_access** deben cumplir los siguientes criterios:  
  
-   Los campos estáticos no se usan para almacenar información. Se permiten los campos estáticos de solo lectura.  
  
-   Se pasa la prueba PEVerify. La herramienta PEVerify (peverify.exe), que comprueba que el código MSIL y los metadatos asociados cumplen los requisitos de seguridad de tipos, se proporciona con .NET Framework SDK.  
  
-   La sincronización, por ejemplo con la clase **SynchronizationAttribute** , no se utiliza.  
  
-   No se usan métodos de finalizador.  
  
 No se permiten los siguientes atributos personalizados en los ensamblados **external_access** :  
  
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
  
-   Se comprueban todas las condiciones del ensamblado **external_access** .  
  
## <a name="runtime-checks"></a>Comprobaciones en tiempo de ejecución  
 En tiempo de ejecución, el ensamblado de código se comprueba para las condiciones siguientes. Si se encuentra cualquiera de estas condiciones, el código administrado no se puede ejecutar y se iniciará una excepción.  
  
### <a name="unsafe"></a>UNSAFE  
 Cargar un ensamblado: ya sea explícitamente llamando al método **System. Reflection. Assembly. Load ()** desde una matriz de bytes o implícitamente mediante el uso del espacio de nombres Reflection **. Emit** , no se permite.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Se comprueban todas las condiciones **no seguras** .  
  
 Todos los tipos y métodos anotados con los siguientes valores de atributo de protección de host (HPA) en la lista compatible de ensamblados no están admitidos.  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Sincronización  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 Para obtener más información sobre hPa y una lista de tipos y miembros no permitidos en los ensamblados admitidos, vea [atributos de protección del host y programación de la integración CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Se comprueban todas las condiciones de **external_access** .  
  
## <a name="see-also"></a>Vea también  
 [Bibliotecas de .NET Framework compatibles](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [Seguridad de acceso del código de integración CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Atributos de protección del host y programación de la integración CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Crear un ensamblado](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
