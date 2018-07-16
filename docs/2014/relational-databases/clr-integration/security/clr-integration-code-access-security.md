---
title: CLR Integration Code Access Security | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
caps.latest.revision: 28
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c2e0d51e1c3268fd7399467f22fb833e77f14131
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349887"
---
# <a name="clr-integration-code-access-security"></a>Seguridad de acceso del código de integración CLR
  Common Language Runtime (CLR) admite un modelo de seguridad denominado seguridad de acceso del código para el código administrado. En este modelo, se conceden permisos a los ensamblados basados en la identidad del código. Para obtener más información, vea la sección sobre seguridad de acceso del código en el kit de desarrollo de software de .NET Framework.  
  
 La directiva de seguridad que determina los permisos que se conceden a los ensamblados se define en tres sitios distintos:  
  
-   Directiva de equipo: es la directiva activa para todo el código administrado que se ejecuta en el equipo donde está instalado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Directiva de usuario: es la directiva activa para el código administrado que se hospeda en un proceso. Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servicio se está ejecutando.  
  
-   Directiva de host: es la directiva configurada por el host de CLR (en este caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) que está activa para el código administrado que se ejecuta en ese host.  
  
 El mecanismo de seguridad de acceso del código admitido por CLR se basa en el supuesto de que el tiempo de ejecución puede hospedar código de plena confianza y código de confianza parcial. Los recursos que están protegidos por la seguridad de acceso del código CLR normalmente se encapsulan las interfaces de programación de aplicaciones administradas que requirethe correspondiente permiso antes de permitir el acceso al recurso. El permiso demandfor solamente se satisface si todos los llamadores (en el nivel de ensamblado) en la pila de llamadas tienen el permiso de recurso correspondiente.  
  
 El conjunto de permisos de seguridad de acceso del código que se conceden al código administrado cuando se ejecuta en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede un conjunto de permisos a un ensamblado cargado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el conjunto de permisos concedidos al código de usuario final puede restringirse más mediante el el usuario y las directivas de nivel de equipo.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Conjuntos de permisos de nivel de directiva de host de SQL Server  
 El conjunto de permisos de seguridad de acceso del código que se concede a los ensamblados mediante el nivel de directiva de host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene determinado por el conjunto de permisos especificado al crear el ensamblado. Hay tres conjuntos de permisos: `SAFE`, `EXTERNAL_ACCESS` y `UNSAFE` (especificado mediante el **PERMISSION_SET** opción de[CREATE ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-assembly-transact-sql)) .  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esta directiva no está pensada para el dominio de aplicación predeterminado que estaría activo cuando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crea una instancia de CLR.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fixedpolicy para ensamblados del sistema y la directiva especificada por el usuario para ensamblados de usuario.  
  
 La directiva fija para ensamblados CLR y ensamblados del sistema de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] les concede plena confianza.  
  
 La parte especificada por el usuario de la directiva de host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] depende de que el propietario de los ensamblados especifique uno de los tres depósitos de permisos para cada ensamblado. Para obtener más información acerca de los permisos de seguridad que se muestran a continuación, vea el SDK de .NET Framework.  
  
### <a name="safe"></a>SAFE  
 Solo se permiten el cálculo interno y el acceso a datos local. `SAFE` es el conjunto de permisos más restrictivo. El código que ejecuta un ensamblado con permisos `SAFE` no puede tener acceso a recursos externos del sistema, como archivos, la red, variables de entorno o el Registro.  
  
 Los ensamblados `SAFE` tienen los siguientes permisos y valores:  
  
|Permiso|Valor(es)/descripción|  
|----------------|-----------------------------|  
|`SecurityPermission`|`Execution:` permiso para ejecutar el código administrado.|  
|`SqlClientPermission`|`Context connection = true`, `context connection = yes`: solo puede usarse la conexión de contexto (context-connection) y la cadena de conexión solo puede especificar un valor "context connection=true" o "context connection=yes".<br /><br /> **AllowBlankPassword = false:** no se permiten contraseñas en blanco.|  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Los ensamblados EXTERNAL_ACCESS tienen los mismos permisos que `SAFE` ensamblados, con la capacidad adicional para tener acceso a recursos externos del sistema como archivos, redes, variables de entorno y el registro.  
  
 Los ensamblados `EXTERNAL_ACCESS` también tienen los siguientes permisos y valores:  
  
|Permiso|Valor(es)/descripción|  
|----------------|-----------------------------|  
|`DistributedTransactionPermission`|`Unrestricted:` Se admiten transacciones distribuidas.|  
|`DNSPermission`|`Unrestricted:` Permiso para solicitar información de servidores de nombres de dominio.|  
|`EnvironmentPermission`|`Unrestricted:` se permite un acceso total a las variables de entorno del sistema y del usuario.|  
|`EventLogPermission`|`Administer:` se permiten las acciones siguientes: crear un origen de eventos, leer los registros existentes, eliminar orígenes o registros de eventos, responder a entradas, borrar un registro de eventos, escuchar eventos y obtener acceso a una colección de todos los registros de eventos.|  
|`FileIOPermission`|`Unrestricted:` se permite un acceso total a los archivos y carpetas.|  
|`KeyContainerPermission`|`Unrestricted:` se permite un acceso total a los contenedores de claves.|  
|`NetworkInformationPermission`|`Access:` se permite hacer ping.|  
|`RegistryPermission`|Permite derechos de lectura de `HKEY_CLASSES_ROOT`, `HKEY_LOCAL_MACHINE`, `HKEY_CURRENT_USER`, `HKEY_CURRENT_CONFIG` y `HKEY_USERS.`|  
|`SecurityPermission`|`Assertion:` posibilidad de afirmar que todos los autores de llamadas de este código tienen el permiso necesario para la operación.<br /><br /> `ControlPrincipal:` posibilidad de manipular el objeto principal.<br /><br /> `Execution:` permiso para ejecutar el código administrado.<br /><br /> `SerializationFormatter:` posibilidad de ofrecer servicios de serialización.|  
|**SmtpPermission**|`Access:` se permiten conexiones salientes al puerto 25 del host SMTP.|  
|`SocketPermission`|`Connect:` se permiten conexiones salientes (todos los puertos, todos los protocolos) en una dirección de transporte.|  
|`SqlClientPermission`|`Unrestricted:` se permite un acceso total al origen de datos.|  
|`StorePermission`|`Unrestricted:` se permite un acceso total a los almacenes de certificados X.509.|  
|`WebPermission`|`Connect:` se permiten conexiones salientes a recursos web.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE permite a los ensamblados un acceso sin límites a los recursos situados tanto dentro como fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El código que se ejecuta desde un ensamblado `UNSAFE` también puede llamar a código no administrado.  
  
 A los ensamblados `UNSAFE` se les concede `FullTrust`.  
  
> [!IMPORTANT]  
>  `SAFE` es la configuración de permiso recomendada para los ensamblados que realizan tareas de administración de datos y cálculos sin tener acceso a los recursos fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. `EXTERNAL_ACCESS` los ensamblados de forma predeterminada se ejecutan como la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuenta de servicio, permiso para ejecutar `EXTERNAL_ACCESS` sólo debería concederse a los inicios de sesión de confianza para ejecutarse como la cuenta de servicio. Desde el punto de vista de la seguridad, los ensamblados `EXTERNAL_ACCESS` y `UNSAFE` son idénticos. Sin embargo, los ensamblados `EXTERNAL_ACCESS` proporcionan diferentes protecciones de confiabilidad y solidez que no se incluyen en los ensamblados `UNSAFE`. Especificar `UNSAFE` permite que el código en el ensamblado para realizar operaciones ilegales en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información acerca de cómo crear ensamblados CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [administrar ensamblados de integración de CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Obtener acceso a recursos externos  
 Si un tipo definido por el usuario (UDT), un procedimiento almacenado u otro tipo de ensamblado de construcción se registra con el conjunto de permisos `SAFE`, el código administrado que se ejecuta en la construcción no puede obtener acceso a los recursos externos. Sin embargo, si se especifica cualquiera de los conjuntos de permisos `EXTERNAL_ACCESS` o `UNSAFE` y el código administrado intenta obtener acceso a recursos externos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica las reglas siguientes:  
  
|Si|Entonces|  
|--------|----------|  
|El contexto de ejecución corresponde a un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|Se deniegan los intentos de acceso a recursos externos y se inicia una excepción de seguridad.|  
|El contexto de ejecución corresponde a un inicio de sesión de Windows y el contexto de ejecución es el autor de la llamada original.|Se obtiene acceso al recurso externo en el contexto de seguridad de la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|El autor de llamada no es el autor de llamada original.|Se deniega el acceso y se inicia una excepción de seguridad.|  
|El contexto de ejecución corresponde a un inicio de sesión de Windows y el contexto de ejecución es el autor de llamada original, y el autor de llamada ha sido suplantado.|El acceso usa el contexto de seguridad del autor de llamada, no la cuenta de servicio.|  
  
## <a name="permission-set-summary"></a>Resumen del conjunto de permisos  
 En el gráfico siguiente se resumen las restricciones y los permisos concedidos a los conjuntos de permisos `SAFE`, `EXTERNAL_ACCESS` y `UNSAFE`.  
  
|||||  
|-|-|-|-|  
||`SAFE`|`EXTERNAL_ACCESS`|`UNSAFE`|  
|`Code Access Security Permissions`|Solo ejecución|Ejecución + acceso a recursos externos|Sin restringir (se incluye P/Invoke)|  
|`Programming model restrictions`|Sí|Sí|Sin restricciones|  
|`Verifiability requirement`|Sí|Sí|no|  
|`Local data access`|Sí|Sí|Sí|  
|`Ability to call native code`|no|no|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de la integración CLR](clr-integration-security.md)   
 [Atributos de protección de host y programación de la integración CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restricciones del modelo de programación de integración de CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Entorno hospedado CLR](../clr-integration-architecture-clr-hosted-environment.md)  
  
  
