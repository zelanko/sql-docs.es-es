---
title: Operadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- operators (users) [Database Engine]
- fail-safe operator [SQL Server]
- aliases [SQL Server], operators
- SQL Server Agent alerts, operators
- contact information [SQL Server Agent]
- net send [SQL Server]
- e-mail [SQL Server], SQL Server Agent operators
- pager notifications [SQL Server Agent]
- mail [SQL Server], SQL Server Agent operators
- operators (users) [Database Engine], defining
- jobs [SQL Server Agent], operators
- alerts [SQL Server], operators
ms.assetid: 38e8488f-2669-4cea-b9c3-5f394a663678
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1a8686722244e107aba20168c63375ba09da5de3
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2019
ms.locfileid: "67685535"
---
# <a name="operators"></a>Operadores
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Los operadores son alias para personas o grupos que pueden recibir una notificación electrónica cuando los trabajos se completan o se activa una alerta. El servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la notificación de administradores a través de operadores. Los operadores habilitan las capacidades de notificación y supervisión del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="operator-attributes-and-concepts"></a>Atributos y conceptos de operador  
Los atributos principales de un operador son:  
  
-   Nombre del operador  
  
-   Información de contacto  
  
### <a name="naming-an-operator"></a>Asignar nombres a operadores  
Cada operador debe tener asignado un nombre. Los nombres de los operadores deben ser únicos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y no pueden tener más de **128** caracteres.  
  
### <a name="contact-information"></a>Información de contacto  
La información de contacto de un operador define cómo se va a notificar a dicho operador. Se puede notificar a los operadores mediante correo electrónico, buscapersonas o con el comando **net send** :  
  
> [!IMPORTANT]
> Las opciones Buscapersonas y **net send** se quitarán del Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una versión futura de [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite utilizar estas características en los nuevos trabajos de programación y planee modificar las aplicaciones que actualmente las utilizan.  
  
-   **Notificación mediante correo electrónico**  
  
    La notificación por correo electrónico envía un mensaje de correo electrónico al operador. Para la notificación por correo electrónico debe proporcionar una dirección de correo electrónico al operador.  
  
-   **Notificación mediante buscapersonas**  
  
    Este tipo de notificación se implementa mediante el correo electrónico. Para la notificación por buscapersonas debe proporcionar una dirección de correo electrónico en la que el operador recibirá los mensajes del buscapersonas. Para establecer la notificación mediante buscapersonas, debe instalar en el servidor de correo un software que procese el correo entrante y lo convierta en mensajes de buscapersonas. El software realizar diversas acciones, entre las que se incluyen:  
  
    -   Reenviar el correo a un servidor de correo remoto en el sitio del proveedor del buscapersonas.  
  
        El proveedor del buscapersonas debe ofrecer este servicio, aunque el software necesario generalmente está disponible como parte del sistema de correo local. Para obtener más información, vea la documentación del buscapersonas.  
  
    -   Enrutar el correo electrónico mediante Internet a un servidor de correo electrónico en el sitio del proveedor del buscapersonas.  
  
        Es una variación del primer planteamiento.  
  
    -   Procesar el mensaje de correo electrónico de entrada y llamar al número del buscapersonas mediante un módem conectado.  
  
        Este software es propiedad de los proveedores de servicios de localización. El software funciona como un cliente de correo electrónico que procesa periódicamente su bandeja de entrada mediante la interpretación de toda o parte de la información de la dirección de correo electrónico como un número de buscapersonas o mediante la correspondencia del nombre de correo electrónico con un número de buscapersonas en una tabla de traducción.  
  
        Si todos los operadores comparten el mismo proveedor de buscapersonas, puede utilizar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para especificar el formato especial de correo electrónico necesario para el sistema de conversión del buscapersonas a correo electrónico. El formato especial puede ser un prefijo o un sufijo y puede incluirse en las siguientes líneas del mensaje de correo electrónico:  
  
        **Asunto:**  
  
        **CC**:  
  
        **Para**:  
  
    > [!NOTE]  
    > Si utiliza un sistema de localización alfanumérica de baja capacidad, puede reducir el texto enviado si excluye el texto del error de la notificación del buscapersonas. Un sistema de localización alfanumérica de baja capacidad es, por ejemplo, uno que esté limitado a 64 caracteres por página.  
  
-   **net sendnotification**  
  
    Envía un mensaje al operador mediante el comando **net send** . Si usa **net send**, especifique el destinatario (el equipo o el usuario) de un mensaje de red.  
  
    > [!NOTE]  
    > El comando **net send** usa Microsoft Windows Messenger. Para enviar alertas correctamente, este servicio debe ejecutarse tanto en el equipo en el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando como en el equipo que usa el operador.  
  
## <a name="alerting-and-fail-safe-operators"></a>Alertas y operadores para notificaciones de error  
Puede elegir a qué operadores notificará en respuesta a una alerta. Por ejemplo, puede asignar responsabilidades rotativas para notificar a los operadores mediante la programación de alertas. Por ejemplo, se notifica a A de las alertas que se producen los lunes, miércoles o viernes, y a B de las que se producen los martes, jueves y sábados.  
  
El operador para notificaciones de error recibe la notificación de una alerta después de que no se haya recibido respuesta a ninguna de las notificaciones enviadas mediante buscapersonas a los operadores designados. Por ejemplo, si ha definido tres operadores para las notificaciones mediante buscapersonas y no se pueden enviar mensajes al buscapersonas de ninguno de ellos, entonces se notificará al operador para notificaciones de error.  
  
Se notifica al operador para notificaciones de error cuando:  
  
-   No se pueden enviar mensajes al localizador de ninguno de los operadores responsables de la alerta.  
  
    Entre los motivos que impiden contactar con los operadores principales se incluyen el uso de direcciones de buscapersonas incorrectas y los operadores fuera de servicio.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente no puede tener acceso a las tablas del sistema en la base de datos **msdb** .  
  
    La tabla del sistema **sysnotifications** especifica las responsabilidades de los operadores respecto a las alertas.  
  
El operador para notificaciones de error es una característica de seguridad. Para eliminar el operador asignado al servicio a prueba de errores debe reasignar el servicio a otro operador o eliminar completamente la asignación a prueba de errores.  
  
## <a name="notifying-an-operator"></a>Notificación de un operador  
Debe configurar al menos uno de los elementos siguientes para poder notificar a un operador:  
  
-   Para enviar un mensaje de correo electrónico mediante la funcionalidad Correo electrónico de base de datos, debe tener acceso a un servidor de correo electrónico que admita SMTP.  
  
-   Para notificar mediante un buscapersonas, debe disponer de hardware o software de otros fabricantes para enviar mensajes de buscapersonas a correo electrónico.  
  
-   Para usar **net send**, el operador debe haber iniciado sesión en el equipo especificado y el equipo especificado debe permitir la recepción de mensajes desde Windows Messenger.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Tareas**|**Tema**|  
|Tareas relacionadas con la creación de un operador|[Crear un operador](../../ssms/agent/create-an-operator.md)<br /><br />[Designate a Fail-Safe Operator](../../ssms/agent/designate-a-fail-safe-operator.md)|  
|Tareas relacionadas con la asignación de alertas|[Asignar alertas a un operador](../../ssms/agent/assign-alerts-to-an-operator.md)<br /><br />[Definir la respuesta a una alerta &#40;SQL Server Management Studio&#41;](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)<br /><br />[sp_add_notification (Transact-SQL)](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)<br /><br />[Asignar alertas a un operador](../../ssms/agent/assign-alerts-to-an-operator.md)|  
  
## <a name="see-also"></a>Consulte también  
[Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)  
  
