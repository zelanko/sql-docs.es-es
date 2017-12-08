---
title: "Configurar la seguridad de diálogo para notificaciones de eventos | Microsoft Docs"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: service-broker
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: event notifications [SQL Server], security
ms.assetid: 12afbc84-2d2a-4452-935e-e1c70e8c53c1
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b1245278976e4befc38913410d1769bcfeadd1f0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="configure-dialog-security-for-event-notifications"></a>Configurar la seguridad de diálogo para notificaciones de eventos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] [!INCLUDE[ssSB](../../includes/sssb-md.md)] se debe configurar para las notificaciones de eventos que envíen mensajes a Service Broker en un servidor remoto. La seguridad de diálogo se debe configurar manualmente según el modelo de seguridad de diálogo completa de [!INCLUDE[ssSB](../../includes/sssb-md.md)] . El modelo de seguridad completa habilita el cifrado y el descifrado de los mensajes que se envían a servidores remotos o desde los mismos. Aunque las notificaciones de eventos se envían en una dirección, otros mensajes, como los errores, también se devuelven en la dirección opuesta.  
  
## <a name="configuring-dialog-security-for-event-notifications"></a>Configurar la seguridad de diálogo para notificaciones de eventos  
 El proceso necesario para implementar la seguridad de diálogo para notificaciones de eventos se describe en los siguientes pasos. Estos pasos incluyen acciones que se han de realizar tanto en el servidor de origen como en el servidor de destino. El servidor de origen es el servidor en el que se crea la notificación de eventos. El servidor de destino es el servidor que recibe el mensaje de notificación de eventos. Debe completar las acciones de cada paso tanto en el servidor de origen como en el de destino antes de poder continuar con el siguiente paso.  
  
> [!IMPORTANT]  
>  Todos los certificados deben crearse con fechas de inicio y de expiración válidas.  
  
 **Paso 1: establezca un número de puerto TCP y un nombre del servicio de destino.**  
  
 Establezca un puerto TCP en el que tanto el servidor de origen como el de destino recibirán los mensajes. Asimismo, debe determinar el nombre del servicio de destino.  
  
 **Paso 2: configure el cifrado y los certificados compartidos para la autenticación en la base de datos.**  
  
 Complete las siguientes acciones en el servidor de origen y en el de destino.  
  
|Servidor de origen|Servidor de destino|  
|-------------------|-------------------|  
|Elija o cree una base de datos para que incluya la notificación de evento y la clave maestra.|Elija o cree una base de datos para que incluya la clave maestra.|  
|Si no existe una clave maestra para la base de datos de origen, [cree una clave maestra](../../t-sql/statements/create-master-key-transact-sql.md). La clave maestra es necesaria en la base de datos de origen y en la de destino para ayudar a proteger sus certificados respectivos.|Si no existe una clave maestra para la base de datos de destino, cree una clave maestra.|  
|[Cree un inicio de sesión](../../t-sql/statements/create-login-transact-sql.md) y el [usuario](../../t-sql/statements/create-user-transact-sql.md) correspondiente para la base de datos de origen.|Cree un inicio de sesión y el usuario correspondiente para la base de datos de destino.|  
|[Cree un certificado](../../t-sql/statements/create-certificate-transact-sql.md) cuyo propietario sea el usuario de la base de datos de origen.|Cree un certificado cuyo propietario sea el usuario de la base de datos de destino.|  
|[Realice una copia de seguridad del certificado](../../t-sql/statements/backup-certificate-transact-sql.md) en un archivo al que se pueda obtener acceso a través del servidor de destino.|Realice una copia de seguridad del certificado en un archivo al que se pueda obtener acceso a través del servidor de origen.|  
|[Cree un usuario](../../t-sql/statements/create-user-transact-sql.md), especificando el usuario de la base de datos de destino y WITHOUT LOGIN. El usuario será el propietario del certificado de la base de datos de destino que se creará a partir del archivo de la copia de seguridad. No es necesario que el usuario esté asignado a un inicio de sesión, puesto que el único propósito del usuario es poseer el certificado de la base de datos de destino creado en el paso 3 que viene a continuación.|Cree un usuario, especificando el usuario de la base de datos de origen y WITHOUT LOGIN. El usuario será el propietario del certificado de la base de datos de origen que se creará a partir del archivo de la copia de seguridad. No es necesario que el usuario esté asignado a un inicio de sesión, puesto que el único propósito del usuario es poseer el certificado de la base de datos de origen creado en el paso 3 que viene a continuación.|  
  
 **Paso 3: comparta los certificados y conceda permisos para la autenticación en la base de datos.**  
  
 Complete las siguientes acciones en el servidor de origen y en el de destino.  
  
|Servidor de origen|Servidor de destino|  
|-------------------|-------------------|  
|[Cree un certificado](../../t-sql/statements/create-certificate-transact-sql.md) a partir de la copia de seguridad del certificado de destino, especificando que el usuario de la base de datos de destino es el propietario.|Cree un certificado a partir del archivo de copia de seguridad del certificado de origen, especificando que el usuario de la base de datos de origen es el propietario.|  
|[Conceda permiso](../../t-sql/statements/grant-transact-sql.md) para crear la notificación de eventos al usuario de la base de datos de origen. Para obtener más información sobre este permiso, vea [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md).|Conceda el permiso REFERENCES al usuario de la base de datos de destino en un contrato de notificaciones de eventos existente de [!INCLUDE[ssSB](../../includes/sssb-md.md)] : `http://schemas.microsoft.com/SQL/Notifications/PostEventNotification`.|  
|[Cree un enlace de servicio remoto](../../t-sql/statements/create-remote-service-binding-transact-sql.md) con el servicio de destino y especifique las credenciales del usuario de la base de datos de destino. El enlace de servicio remoto garantiza que la clave pública del certificado propiedad del usuario de la base de datos de origen autenticará los mensajes que se envíen al servidor de destino.|[Conceda](../../t-sql/statements/grant-transact-sql.md) permisos CREATE QUEUE, CREATE SERVICE y CREATE SCHEMA al usuario de la base de datos de destino.|  
||Si todavía no lo ha hecho, conéctese ahora con la base de datos como usuario de la base de datos de destino.|  
||[Cree una cola](../../t-sql/statements/create-queue-transact-sql.md) para recibir los mensajes de notificación de eventos y [cree un servicio](../../t-sql/statements/create-service-transact-sql.md) para entregar los mensajes.|  
||[Conceda el permiso SEND](../../t-sql/statements/grant-transact-sql.md) para el servicio de destino al usuario de la base de datos de origen.|  
|Proporcione el identificador de Service Broker de la base de datos de origen al servidor de destino. Este identificador se puede obtener realizando una consulta en la columna **service_broker_guid** de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) . En caso de una notificación de eventos en el servidor, use el identificador de Service Broker de **msdb**.|Proporcione el identificador de Service Broker de la base de datos de destino al servidor de origen.|  
  
 **Paso 4: cree rutas y establezca la autenticación en el servidor.**  
  
 Complete las siguientes acciones en el servidor de origen y en el de destino.  
  
|Servidor de origen|Servidor de destino|  
|-------------------|-------------------|  
|[Cree una ruta](../../t-sql/statements/create-route-transact-sql.md) al servicio de destino y especifique el identificador de Service Broker de la base de datos de destino y el número de puerto TCP acordado.|Cree una ruta al servicio de origen y especifique el identificador de Service Broker de la base de datos de origen y el número de puerto TCP acordado. Utilice el siguiente servicio suministrado para especificar el servicio de origen: `http://schemas.microsoft.com/SQL/Notifications/EventNotificationService`.|  
|Cambie a la base de datos **maestra** para configurar la autenticación en el servidor.|Cambie a la base de datos **maestra** para configurar la autenticación en el servidor.|  
|Si no existe una clave maestra para la base de datos **master** , [cree una clave maestra](../../t-sql/statements/create-master-key-transact-sql.md).|Si no existe una clave maestra para la base de datos **master** , cree una clave maestra.|  
|[Cree un certificado](../../t-sql/statements/create-certificate-transact-sql.md) para autenticar la base de datos.|Cree un certificado para autenticar la base de datos.|  
|[Realice una copia de seguridad del certificado](../../t-sql/statements/backup-certificate-transact-sql.md) en un archivo al que se pueda obtener acceso a través del servidor de destino.|Realice una copia de seguridad del certificado en un archivo al que se pueda obtener acceso a través del servidor de origen.|  
|[Cree un punto de conexión](../../t-sql/statements/create-endpoint-transact-sql.md)y especifique el número de puerto TCP acordado, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *nombre_de_certificado*) y el nombre del certificado que proporciona la autenticación.|Cree un punto de conexión y especifique el número de puerto TCP acordado, FOR SERVICE_BROKER (AUTHENTICATION = CERTIFICATE *nombre_de_certificado*) y el nombre del certificado que proporciona la autenticación.|  
|[Cree un inicio de sesión](../../t-sql/statements/create-login-transact-sql.md)y especifique el inicio de sesión del servidor de destino.|Cree un inicio de sesión y especifique el inicio de sesión del servidor de origen.|  
|[Conceda el permiso CONNECT](../../t-sql/statements/grant-transact-sql.md) para el extremo al inicio de sesión del autenticador de destino.|Conceda el permiso CONNECT para el extremo al inicio de sesión del autenticador de origen.|  
|[Cree un usuario](../../t-sql/statements/create-user-transact-sql.md)y especifique el inicio de sesión del autenticador de destino.|Cree un usuario y especifique el inicio de sesión del autenticador de origen.|  
  
 **Paso 5: comparta certificados para la autenticación en el servidor y cree la notificación de eventos.**  
  
 Complete las siguientes acciones en el servidor de origen y en el de destino.  
  
|Servidor de origen|Servidor de destino|  
|-------------------|-------------------|  
|[Cree un certificado](../../t-sql/statements/create-certificate-transact-sql.md) a partir de la copia de seguridad del certificado de destino, especificando que el usuario autenticador de destino es el propietario.|Cree un certificado a partir de la copia de seguridad del certificado de origen, especificando que el usuario autenticador de origen es el propietario.|  
|Cambie a la base de datos de origen en la que va a crear la notificación de eventos y, si todavía no está conectado como usuario de la base de datos de origen, hágalo ahora.|Cambie a la base de datos de destino para recibir los mensajes de notificación de eventos.|  
|[Cree la notificación de eventos](../../t-sql/statements/create-event-notification-transact-sql.md)y especifique el Service Broker y el identificador de la base de datos de origen.||  
  
## <a name="see-also"></a>Vea también  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Implementar notificaciones de eventos](../../relational-databases/service-broker/implement-event-notifications.md)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](../../t-sql/statements/create-remote-service-binding-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)   
 [CREATE EVENT NOTIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-notification-transact-sql.md)  
  
  
