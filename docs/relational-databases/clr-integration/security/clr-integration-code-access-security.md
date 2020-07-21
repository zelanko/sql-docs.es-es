---
title: Seguridad de acceso del código de integración CLR | Microsoft Docs
description: Para la integración de SQL Server CLR, CLR admite la seguridad de acceso del código para el código administrado, donde se conceden permisos a los ensamblados en función de la identidad del código.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- UNSAFE assemblies
- permissions [CLR integration]
- common language runtime [SQL Server], security
- SAFE assemblies
- code access security [CLR integration]
- EXTERNAL_ACCESS assemblies
ms.assetid: 2111cfe0-d5e0-43b1-93c3-e994ac0e9729
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e155e9c6f0e8a85eaf7ec905f9c9b471160a9ec
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85885899"
---
# <a name="clr-integration-code-access-security"></a>Seguridad de acceso del código de integración CLR
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Common Language Runtime (CLR) admite un modelo de seguridad denominado seguridad de acceso del código para el código administrado. En este modelo, se conceden permisos a los ensamblados basados en la identidad del código. Para obtener más información, vea la sección sobre seguridad de acceso del código en el kit de desarrollo de software de .NET Framework.  
  
 La directiva de seguridad que determina los permisos que se conceden a los ensamblados se define en tres sitios distintos:  
  
-   Directiva de equipo: es la directiva activa para todo el código administrado que se ejecuta en el equipo donde está instalado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Directiva de usuario: es la directiva activa para el código administrado que se hospeda en un proceso. Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la directiva de usuario es específica de la cuenta de Windows en la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Directiva de host: es la directiva configurada por el host de CLR (en este caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) que está activa para el código administrado que se ejecuta en ese host.  
  
 El mecanismo de seguridad de acceso del código admitido por CLR se basa en el supuesto de que el tiempo de ejecución puede hospedar código de plena confianza y código de confianza parcial. Los recursos protegidos por la seguridad de acceso del código de CLR suelen empaquetarse mediante interfaces de programación de aplicaciones que requieren el permiso correspondiente antes de permitir el acceso al recurso. La solicitud de permiso solo se satisface si todos los que llaman (en el nivel de ensamblado) de la pila de llamadas tienen el permiso correspondiente para el recurso.  
  
 El conjunto de permisos de seguridad de acceso del código que se conceden al código administrado cuando se ejecuta en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es la combinación del conjunto de permisos que conceden los tres niveles de directiva mencionados anteriormente. Aunque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conceda un conjunto de permisos a un ensamblado cargado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], las directivas de nivel de usuario y de equipo pueden restringir aún más el posible conjunto de permisos que se concede al código de usuario.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Conjuntos de permisos de nivel de directiva de host de SQL Server  
 El conjunto de permisos de seguridad de acceso del código que se concede a los ensamblados mediante el nivel de directiva de host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene determinado por el conjunto de permisos especificado al crear el ensamblado. Hay tres conjuntos de permisos: **Safe**, **external_access** y **Unsafe** (especificado mediante la opción **PERMISSION_SET** de [Create Assembly &#40;Transact-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona un nivel de directiva de seguridad de nivel de host a CLR mientras lo hospeda; esta directiva es un nivel de directiva adicional por debajo de los dos niveles de directiva que siempre están activos. Esta directiva se establece para cada dominio de aplicación creado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esta directiva no está pensada para el dominio de aplicación predeterminado que estaría activo cuando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crea una instancia de CLR.  
  
 La directiva de nivel de host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es una combinación de la directiva fija de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para ensamblados de sistema y de la directiva especificada por el usuario para ensamblados de usuario.  
  
 La directiva fija para ensamblados CLR y ensamblados del sistema de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] les concede plena confianza.  
  
 La parte especificada por el usuario de la directiva de host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] depende de que el propietario de los ensamblados especifique uno de los tres depósitos de permisos para cada ensamblado. Para obtener más información acerca de los permisos de seguridad que se muestran a continuación, vea el SDK de .NET Framework.  
  
### <a name="safe"></a>SAFE  
 Solo se permiten el cálculo interno y el acceso a datos local. **Safe** es el conjunto de permisos más restrictivo. El código ejecutado por un ensamblado con permisos **seguros** no puede tener acceso a recursos externos del sistema, como archivos, la red, variables de entorno o el registro.  
  
 Los ensamblados **seguros** tienen los siguientes permisos y valores:  
  
|Permiso|Valor(es)/descripción|  
|----------------|-----------------------------|  
|**SecurityPermission**|**Ejecución:** Permiso para ejecutar código administrado.|  
|**SqlClientPermission**|**Conexión de contexto = true**, **conexión de contexto = sí**: solo se puede usar la conexión de contexto y la cadena de conexión solo puede especificar un valor de "context Connection = true" o "context Connection = Yes".<br /><br /> **AllowBlankPassword = false:**  No se permiten contraseñas en blanco.|  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS ensamblados tienen los mismos permisos que los ensamblados **seguros** , con la capacidad adicional para tener acceso a recursos externos del sistema, como archivos, redes, variables de entorno y el registro.  
  
 Los ensamblados de **external_access** también tienen los siguientes permisos y valores:  
  
|Permiso|Valor(es)/descripción|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**Sin restricción:** Se permiten las transacciones distribuidas.|  
|**DNSPermission**|**Sin restricción:** Permiso para solicitar información de servidores de nombres de dominio.|  
|**EnvironmentPermission**|**Sin restricción:** Se permite el acceso total a las variables de entorno del usuario y del sistema.|  
|**EventLogPermission**|**Administrar:** Se permiten las acciones siguientes: crear un origen de eventos, leer los registros existentes, eliminar orígenes o registros de eventos, responder a entradas, borrar un registro de eventos, escuchar eventos y obtener acceso a una colección de todos los registros de eventos.|  
|**Permiso**|**Sin restricción:** Se permite el acceso total a archivos y carpetas.|  
|**KeyContainerPermission**|**Sin restricción:** Se permite el acceso total a los contenedores de claves.|  
|**NetworkInformationPermission**|**Acceso:** Se permite hacer ping.|  
|**RegistryPermission**|Permite derechos de lectura en **HKEY_CLASSES_ROOT**, **HKEY_LOCAL_MACHINE**, **HKEY_CURRENT_USER**, **HKEY_CURRENT_CONFIG**y **HKEY_USERS.**|  
|**SecurityPermission**|**Aserción:** Capacidad de afirmar que todos los llamadores de este código tienen el permiso necesario para la operación.<br /><br /> **ControlPrincipal:** Capacidad de manipular el objeto principal.<br /><br /> **Ejecución:** Permiso para ejecutar código administrado.<br /><br /> **SerializationFormatter:** Capacidad de proporcionar servicios de serialización.|  
|**SmtpPermission**|**Acceso:** Se permiten las conexiones salientes al puerto 25 del host SMTP.|  
|**SocketPermission**|**Conectar:** Se permiten las conexiones salientes (todos los puertos, todos los protocolos) en una dirección de transporte.|  
|**SqlClientPermission**|**Sin restricción:** Se permite el acceso total al origen de los mismos.|  
|**StorePermission**|**Sin restricción:** Se permite el acceso total a los almacenes de certificados X. 509.|  
|**WebPermission**|**Conectar:** Se permiten las conexiones salientes a los recursos Web.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE permite a los ensamblados un acceso sin límites a los recursos situados tanto dentro como fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El código que se ejecuta desde dentro de un ensamblado **no seguro** también puede llamar a código no administrado.  
  
 Los ensamblados **no seguros** reciben **FullTrust**.  
  
> [!IMPORTANT]  
>  **Safe** es la configuración de permisos recomendada para los ensamblados que realizan tareas de administración de datos y cálculo sin tener acceso a recursos fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . **External_access** se recomienda para los ensamblados que tienen acceso a recursos fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . **External_access** ensamblados de forma predeterminada se ejecutan como la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuenta de servicio. Es posible que **external_access** código suplante explícitamente el contexto de seguridad de la autenticación de Windows del llamador. Puesto que el valor predeterminado es ejecutar como la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuenta de servicio, solo se debe conceder permiso para ejecutar **external_access** a los inicios de sesión de confianza para ejecutarse como la cuenta de servicio. Desde la perspectiva de la seguridad, los ensamblados de **external_access** y **no seguros** son idénticos. Sin embargo, los ensamblados de **external_access** proporcionan varias protecciones de confiabilidad y solidez que no están en ensamblados no **seguros** . La especificación de **Unsafe** permite al código del ensamblado realizar operaciones ilegales en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] espacio del proceso y, por lo tanto, puede poner en peligro la solidez y la escalabilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información sobre la creación de ensamblados CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , vea [administrar ensamblados de integración CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Obtener acceso a recursos externos  
 Si un tipo definido por el usuario (UDT), un procedimiento almacenado u otro tipo de ensamblado de construcción se registra con el conjunto de permisos **Safe** , el código administrado que se ejecuta en la construcción no puede tener acceso a los recursos externos. Sin embargo, si se especifican los conjuntos de permisos **external_access** o **Unsafe** , y el código administrado intenta tener acceso a recursos externos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica las siguientes reglas:  
  
|Si|Entonces|  
|--------|----------|  
|El contexto de ejecución corresponde a un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|Se deniegan los intentos de acceso a recursos externos y se inicia una excepción de seguridad.|  
|El contexto de ejecución corresponde a un inicio de sesión de Windows y el contexto de ejecución es el autor de la llamada original.|Se obtiene acceso al recurso externo en el contexto de seguridad de la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|El autor de llamada no es el autor de llamada original.|Se deniega el acceso y se inicia una excepción de seguridad.|  
|El contexto de ejecución corresponde a un inicio de sesión de Windows y el contexto de ejecución es el autor de llamada original, y el autor de llamada ha sido suplantado.|El acceso usa el contexto de seguridad del autor de llamada, no la cuenta de servicio.|  
  
## <a name="permission-set-summary"></a>Resumen del conjunto de permisos  
 En el gráfico siguiente se resumen las restricciones y los permisos concedidos a los conjuntos de permisos **Safe**, **external_access**y **Unsafe** .  
  
|||||  
|-|-|-|-|  
||**SEGURA**|**EXTERNAL_ACCESS**|**NO seguro**|  
|**Permisos de seguridad de acceso del código**|Solo ejecución|Ejecución + acceso a recursos externos|Sin restringir (se incluye P/Invoke)|  
|**Restricciones del modelo de programación**|Sí|Sí|Sin restricciones|  
|**Requisito de capacidad de comprobación**|Sí|Sí|No|  
|**Acceso a datos locales**|Sí|Sí|Sí|  
|**Capacidad de llamar a código nativo**|No|No|Sí|  
  
## <a name="see-also"></a>Consulte también  
 [Seguridad de la integración CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Atributos de protección del host y programación de la integración CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restricciones del modelo de programación de la integración CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Entorno hospedado CLR](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
