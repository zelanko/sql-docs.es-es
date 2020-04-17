---
title: Restricciones del modelo de programación de integración de CLR ? Microsoft Docs
description: SQL ServerSQL Server realiza comprobaciones de código en objetos de base de datos administrados cuando se registran por primera vez mediante CREATE ASSEMBLY y en tiempo de ejecución.
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
ms.openlocfilehash: 83b73909cf1844796640a83910ee609eadd7dba4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488558"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restricciones del modelo de programación de la integración CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Cuando se crea un procedimiento almacenado administrado u otro objeto de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] base de datos administrada, hay ciertas comprobaciones de código realizadas por que deben tenerse en cuenta. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Realiza comprobaciones en el ensamblado de código administrado cuando se registra por primera vez en la base de datos, mediante la instrucción **CREATE ASSEMBLY** y también en tiempo de ejecución. El código administrado también se comprueba en tiempo de ejecución porque en un ensamblado puede haber rutas de acceso al código que nunca se hayan alcanzado realmente en tiempo de ejecución.  Esto proporciona flexibilidad para registrar ensamblados de terceros, de manera especial, de forma que no se debe bloquear un ensamblado donde haya un código 'no seguro' diseñado para que se ejecute en un entorno cliente pero nunca se ejecutaría en el CLR hospedado. Los requisitos que debe cumplir el código administrado dependen de si el ensamblado está registrado como **SAFE**, **EXTERNAL_ACCESS**o **UNSAFE**, **SAFE** es el más estricto y se enumeran a continuación.  
  
 Además de las restricciones que se ubican en los ensamblados de código administrado, también hay permisos de seguridad de código que se conceden. Common Language Runtime (CLR) admite un modelo de seguridad denominado seguridad de acceso del código (CAS) para el código administrado. En este modelo, se conceden permisos a los ensamblados basados en la identidad del código. **LOS**ensamblados SAFE , **EXTERNAL_ACCESS**y **UNSAFE** tienen diferentes permisos CAS. Para obtener más información, vea Seguridad de acceso a código de [integración de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Comprobaciones de CREATE ASSEMBLY  
 Cuando se ejecuta la instrucción **CREATE ASSEMBLY,** se realizan las siguientes comprobaciones para cada nivel de seguridad.  Si se produce un error en cualquier comprobación, **CREATE ASSEMBLY** producirá un error con un mensaje de error.  
  
### <a name="global-any-security-level"></a>Global (cualquier nivel de seguridad)  
 Todos los ensamblados a los que se hace referencia deben cumplir uno o más de los criterios siguientes:  
  
-   El ensamblado ya está registrado en la base de datos.  
  
-   El ensamblado es uno de los ensamblados compatibles. Para obtener más información, vea Bibliotecas de [.NET Framework compatibles](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
-   Está utilizando **CREATE ASSEMBLY FROM**_\<>_ de ubicación y todos los ensamblados a los que se hace referencia y sus dependencias están disponibles en * \<la ubicación>*.  
  
-   Está utilizando **CREATE ASSEMBLY FROM**_\<bytes ...>,_ y todas las referencias se especifican a través de bytes separados por espacios.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Todos los ensamblados **EXTERNAL_ACCESS** deben cumplir los siguientes criterios:  
  
-   Los campos estáticos no se usan para almacenar información. Se permiten los campos estáticos de solo lectura.  
  
-   Se pasa la prueba PEVerify. La herramienta PEVerify (peverify.exe), que comprueba que el código MSIL y los metadatos asociados cumplen los requisitos de seguridad de tipos, se proporciona con .NET Framework SDK.  
  
-   La sincronización, por ejemplo con la clase **SynchronizationAttribute,** no se utiliza.  
  
-   No se usan métodos de finalizador.  
  
 Los siguientes atributos personalizados no se permiten en **EXTERNAL_ACCESS** ensamblados:  
  
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
  
-   Se comprueban todas las condiciones de ensamblaje **EXTERNAL_ACCESS.**  
  
## <a name="runtime-checks"></a>Comprobaciones en tiempo de ejecución  
 En tiempo de ejecución, el ensamblado de código se comprueba para las condiciones siguientes. Si se encuentra cualquiera de estas condiciones, el código administrado no se puede ejecutar y se iniciará una excepción.  
  
### <a name="unsafe"></a>UNSAFE  
 No se permite cargar un ensamblado explícitamente llamando al método **System.Reflection.Assembly.Load()** desde una matriz de bytes o implícitamente mediante el uso del espacio de nombres **Reflection.Emit.**  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Se comprueban todas las condiciones de **UNSAFE.**  
  
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
  
 Para obtener más información acerca de los HPA y una lista de tipos y miembros no permitidos en los ensamblados admitidos, vea Atributos de protección de host y Programación de [integración de CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Se comprueban todas las condiciones **EXTERNAL_ACCESS.**  
  
## <a name="see-also"></a>Consulte también  
 [Bibliotecas de .NET Framework compatibles](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [Seguridad de acceso al código de integración de CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Atributos de protección de host y programación de integración de CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Crear un ensamblado](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
