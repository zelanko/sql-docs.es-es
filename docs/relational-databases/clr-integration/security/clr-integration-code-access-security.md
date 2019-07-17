---
title: CLR Integration Code Access Security | Microsoft Docs
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
ms.openlocfilehash: f49968392dd813b48f43e5e63586fd0c6bec71d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118515"
---
# <a name="clr-integration-code-access-security"></a>Seguridad de acceso del código de integración CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Common Language Runtime (CLR) admite un modelo de seguridad denominado seguridad de acceso del código para el código administrado. En este modelo, se conceden permisos a los ensamblados basados en la identidad del código. Para obtener más información, vea la sección sobre seguridad de acceso del código en el kit de desarrollo de software de .NET Framework.  
  
 La directiva de seguridad que determina los permisos que se conceden a los ensamblados se define en tres sitios distintos:  
  
-   Directiva de equipo: Esta es la directiva en vigor para todo el código administrado que se ejecuta en el equipo en el que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] está instalado.  
  
-   Directiva de usuario: Esta es la directiva en vigor para código administrado hospedado por un proceso. Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], la directiva de usuario es específica de la cuenta de Windows en la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Directiva de host: Esta es la directiva configurada por el host de CLR (en este caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]) que está en vigor para código administrado que se ejecuta en ese host.  
  
 El mecanismo de seguridad de acceso del código admitido por CLR se basa en el supuesto de que el tiempo de ejecución puede hospedar código de plena confianza y código de confianza parcial. Los recursos que están protegidos por la seguridad de acceso del código CLR se incluyen normalmente en interfaces de programación de aplicación administrada que requieren el permiso correspondiente antes de permitir el acceso al recurso. La solicitud de permiso solo se satisface si todos los que llaman (en el nivel de ensamblado) de la pila de llamadas tienen el permiso correspondiente para el recurso.  
  
 El conjunto de permisos de seguridad de acceso del código que se conceden al código administrado cuando se ejecuta en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es la combinación del conjunto de permisos que conceden los tres niveles de directiva mencionados anteriormente. Aunque [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conceda un conjunto de permisos a un ensamblado cargado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], las directivas de nivel de usuario y de equipo pueden restringir aún más el posible conjunto de permisos que se concede al código de usuario.  
  
## <a name="sql-server-host-policy-level-permission-sets"></a>Conjuntos de permisos de nivel de directiva de host de SQL Server  
 El conjunto de permisos de seguridad de acceso del código que se concede a los ensamblados mediante el nivel de directiva de host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene determinado por el conjunto de permisos especificado al crear el ensamblado. Hay tres conjuntos de permisos: **SEGURO**, **EXTERNAL_ACCESS** y **UNSAFE** (especificado mediante el **PERMISSION_SET** opción de [CREATE ASSEMBLY &#40; Transact-SQL&#41;](../../../t-sql/statements/create-assembly-transact-sql.md)).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proporciona un nivel de directiva de seguridad de nivel de host a CLR mientras lo hospeda; esta directiva es un nivel de directiva adicional por debajo de los dos niveles de directiva que siempre están activos. Esta directiva se establece para cada dominio de aplicación creado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esta directiva no está pensada para el dominio de aplicación predeterminado que estaría activo cuando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] crea una instancia de CLR.  
  
 La directiva de nivel de host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es una combinación de la directiva fija de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para ensamblados de sistema y de la directiva especificada por el usuario para ensamblados de usuario.  
  
 La directiva fija para ensamblados CLR y ensamblados del sistema de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] les concede plena confianza.  
  
 La parte especificada por el usuario de la directiva de host de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] depende de que el propietario de los ensamblados especifique uno de los tres depósitos de permisos para cada ensamblado. Para obtener más información acerca de los permisos de seguridad que se muestran a continuación, vea el SDK de .NET Framework.  
  
### <a name="safe"></a>SAFE  
 Solo se permiten el cálculo interno y el acceso a datos local. **SEGURO** es el conjunto de permisos más restrictivo. El código ejecutado por un ensamblado con **seguro** permisos no pueden obtener acceso a recursos externos del sistema como archivos, la red, las variables de entorno o el registro.  
  
 **SEGURO** ensamblados tienen los permisos y los valores siguientes:  
  
|Permiso|Valor(es)/descripción|  
|----------------|-----------------------------|  
|**SecurityPermission**|**Ejecución:** Permiso para ejecutar código administrado.|  
|**SqlClientPermission**|**Conexión de contexto = true**, **conexión de contexto = yes**: Solo se puede usar la conexión de contexto y la cadena de conexión solo puede especificar un valor de "conexión de contexto = true" o "conexión de contexto = yes".<br /><br /> **AllowBlankPassword = false:**  No se permiten contraseñas en blanco.|  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 Los ensamblados EXTERNAL_ACCESS tienen los mismos permisos que **seguro** ensamblados, con la capacidad adicional para tener acceso a recursos externos del sistema como archivos, redes, variables de entorno y el registro.  
  
 **EXTERNAL_ACCESS** ensamblados también tienen los permisos y los valores siguientes:  
  
|Permiso|Valor(es)/descripción|  
|----------------|-----------------------------|  
|**DistributedTransactionPermission**|**Sin restricciones:** Se admiten transacciones distribuidas.|  
|**DNSPermission**|**Sin restricciones:** Permiso para solicitar información de servidores de nombres de dominio.|  
|**EnvironmentPermission**|**Sin restricciones:** Se permite el acceso completo a las variables de entorno de usuario y del sistema.|  
|**EventLogPermission**|**Administrar:** Se permiten las siguientes acciones: crear un origen de eventos, leer los registros existentes, eliminar orígenes de eventos o registros, responder a entradas, borrar un registro de eventos, escuchar eventos y obtener acceso a una colección de todos los registros de eventos.|  
|**FileIOPermission**|**Sin restricciones:** Se permite un acceso total a archivos y carpetas.|  
|**KeyContainerPermission**|**Sin restricciones:** Se permite el acceso completo a los contenedores de claves.|  
|**NetworkInformationPermission**|**Acceso:** Se permite hacer ping.|  
|**RegistryPermission**|Permite derechos de lectura **HKEY_CLASSES_ROOT**, **HKEY_LOCAL_MACHINE**, **HKEY_CURRENT_USER**, **HKEY_CURRENT_CONFIG**y  **HKEY_USERS.**|  
|**SecurityPermission**|**Aserción:** Posibilidad de afirmar que todos los llamadores de este código tienen el permiso necesario para la operación.<br /><br /> **ControlPrincipal:** Capacidad de manipular el objeto principal.<br /><br /> **Ejecución:** Permiso para ejecutar código administrado.<br /><br /> **SerializationFormatter:** Capacidad para proporcionar servicios de serialización.|  
|**SmtpPermission**|**Acceso:** Se permiten conexiones salientes al puerto 25 del host SMTP.|  
|**SocketPermission**|**Conectar:** Se permiten conexiones salientes (todos los puertos, todos los protocolos) en una dirección de transporte.|  
|**SqlClientPermission**|**Sin restricciones:** Se permite un acceso total al origen de datos.|  
|**StorePermission**|**Sin restricciones:** Se permite un acceso total a los almacenes de certificados X.509.|  
|**WebPermission**|**Conectar:** Se permiten conexiones salientes a recursos web.|  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE permite a los ensamblados un acceso sin límites a los recursos situados tanto dentro como fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Código que se ejecuta desde un **UNSAFE** ensamblado también puede llamar a código no administrado.  
  
 **UNSAFE** ensamblados reciben **FullTrust**.  
  
> [!IMPORTANT]  
>  **SEGURO** es la configuración de permisos recomendada para los ensamblados que realizan tareas de administración de datos y cálculos sin tener acceso a recursos externos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **EXTERNAL_ACCESS** se recomienda para los ensamblados que tienen acceso a recursos externos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **EXTERNAL_ACCESS** ejecutan de forma predeterminada, los ensamblados como los [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuenta de servicio. Es posible que **EXTERNAL_ACCESS** código suplantar explícitamente el contexto de seguridad de autenticación de Windows del llamador. Dado que el valor predeterminado es ejecutarse como la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuenta de servicio, permiso para ejecutar **EXTERNAL_ACCESS** sólo debería concederse a los inicios de sesión de confianza para ejecutarse como la cuenta de servicio. Desde una perspectiva de seguridad, **EXTERNAL_ACCESS** y **UNSAFE** ensamblados son idénticos. Sin embargo, **EXTERNAL_ACCESS** ensamblados proporcionan diferentes protecciones de confiabilidad y solidez que no están en **UNSAFE** ensamblados. Especificar **UNSAFE** permite que el código en el ensamblado para realizar operaciones ilegales en el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] espacio del proceso y, por lo tanto, puede poner en peligro la robustez y escalabilidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información acerca de cómo crear ensamblados CLR en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], consulte [administrar ensamblados de integración de CLR](../../../relational-databases/clr-integration/assemblies/managing-clr-integration-assemblies.md).  
  
## <a name="accessing-external-resources"></a>Obtener acceso a recursos externos  
 Si un tipo definido por el usuario (UDT), procedimiento almacenado u otro tipo de ensamblado de construcción se registra con el **seguro** conjunto de permisos y, después, ejecuta código administrado en la construcción no puede tener acceso a recursos externos. Sin embargo, si bien la **EXTERNAL_ACCESS** o **UNSAFE** conjuntos de permisos se especifican y código administrado intenta obtener acceso a recursos externos, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aplica las reglas siguientes:  
  
|Si|Entonces|  
|--------|----------|  
|El contexto de ejecución corresponde a un inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|Se deniegan los intentos de acceso a recursos externos y se inicia una excepción de seguridad.|  
|El contexto de ejecución corresponde a un inicio de sesión de Windows y el contexto de ejecución es el autor de la llamada original.|Se obtiene acceso al recurso externo en el contexto de seguridad de la cuenta de servicio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|El autor de llamada no es el autor de llamada original.|Se deniega el acceso y se inicia una excepción de seguridad.|  
|El contexto de ejecución corresponde a un inicio de sesión de Windows y el contexto de ejecución es el autor de llamada original, y el autor de llamada ha sido suplantado.|El acceso usa el contexto de seguridad del autor de llamada, no la cuenta de servicio.|  
  
## <a name="permission-set-summary"></a>Resumen del conjunto de permisos  
 El gráfico siguiente resumen las restricciones y los permisos concedidos a la **seguro**, **EXTERNAL_ACCESS**, y **UNSAFE** conjuntos de permisos.  
  
|||||  
|-|-|-|-|  
||**SAFE**|**EXTERNAL_ACCESS**|**NO SEGURO**|  
|**Permisos de seguridad de acceso de código**|Solo ejecución|Ejecución + acceso a recursos externos|Sin restringir (se incluye P/Invoke)|  
|**Restricciones del modelo de programación**|Sí|Sí|Sin restricciones|  
|**Requisito de verificabilidad**|Sí|Sí|Sin|  
|**Acceso a datos locales**|Sí|Sí|Sí|  
|**Posibilidad de llamar a código nativo**|No|Sin|Sí|  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de la integración CLR](../../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Atributos de protección de host y programación de la integración CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Restricciones del modelo de programación de integración de CLR](../../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Entorno hospedado CLR](../../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)  
  
  
