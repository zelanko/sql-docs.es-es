---
title: Correo electrónico de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- architecture [SQL Server], Database Mail
- Database Mail [SQL Server], architecture
- Database Mail [SQL Server], components
ms.assetid: 9e4563dd-4799-4b32-a78a-048ea44a44c1
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 40f485a3e75e02c47e1e0c15e1ab47650040b983
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37285371"
---
# <a name="database-mail"></a>Correo electrónico de base de datos
  El Correo electrónico de base de datos es una solución empresarial para enviar mensajes de correo electrónico desde [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]. El Correo electrónico de base de datos permite a las aplicaciones de base de datos enviar mensajes de correo electrónico a los usuarios. Los mensajes enviados pueden incluir resultados de consultas y archivos de cualquier recurso de la red.  
  
 
  
##  <a name="Benefits"></a> Ventajas de usar el Correo electrónico de base de datos  
 El Correo electrónico de base de datos está diseñado para proporcionar confiabilidad, escalabilidad, seguridad y compatibilidad.  
  
### <a name="reliability"></a>Confiabilidad  
  
-   El Correo electrónico de base de datos usa el protocolo estándar SMTP (Protocolo simple de transferencia de correo) para enviar correo electrónico. Puede utilizar el Correo electrónico de base de datos sin necesidad de instalar un cliente con MAPI extendida en el equipo en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Aislamiento de procesos. Para minimizar el impacto en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el componente que entrega el correo electrónico se ejecuta fuera de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en un proceso independiente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] continuará almacenando en cola los mensajes de correo electrónico incluso si el proceso externo se detiene o genera un error. Los mensajes en cola se enviarán cuando el proceso externo o el servidor SMTP se encuentren en línea.  
  
-   Cuentas de conmutación por error. Los perfiles del Correo electrónico de base de datos permiten especificar más de un servidor SMTP. Si un servidor SMTP no está disponible, se puede enviar el correo mediante otro.  
  
-   Compatibilidad con clústeres. El Correo electrónico de base de datos es una aplicación para clústeres y es totalmente compatible con estos.  
  
### <a name="scalability"></a>Escalabilidad  
  
-   Entrega en segundo plano: el Correo electrónico de base de datos permite realizar entregas en segundo plano o asincrónicas. Cuando se llama a **sp_send_dbmail** para enviar un mensaje, Correo electrónico de base de datos agrega una solicitud a una cola de [!INCLUDE[ssSB](../../includes/sssb-md.md)] . El procedimiento almacenado se devuelve inmediatamente. El componente de correo electrónico externo recibe la solicitud y entrega el mensaje.  
  
-   Varios perfiles: el Correo electrónico de base de datos permite crear varios perfiles en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . También se puede elegir el perfil del Correo electrónico de base de datos para enviar el mensaje.  
  
-   Varias cuentas: cada perfil puede incluir varias cuentas de conmutación por error. Se pueden configurar varios perfiles con distintas cuentas para distribuir el correo electrónico entre varios servidores de correo.  
  
-   Compatibilidad con 64 bits: el Correo electrónico de base de datos es totalmente compatible con las versiones de 64 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="security"></a>Seguridad  
  
-   Desactivado de forma predeterminada: para reducir el área expuesta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los procedimientos almacenados del Correo electrónico de base de datos están deshabilitados de forma predeterminada.  
  
-   Seguridad de correo electrónico: para enviar Correo electrónico de base de datos debe ser miembro del rol de base de datos **DatabaseMailUserRole** en la base de datos **msdb** .  
  
-   Seguridad de perfil: el Correo electrónico de base de datos aplica la seguridad para los perfiles de correo. El usuario elige cuáles son los usuarios o grupos de la base de datos **msdb** que tienen acceso a los perfiles del Correo electrónico de base de datos. Se puede conceder acceso a usuarios específicos o a todos los usuarios de **msdb**. Un perfil privado restringe el acceso a una lista especificada de usuarios. Un perfil público está disponible para todos los usuarios de la base de datos.  
  
-   Regulador del tamaño de los datos adjuntos: el Correo electrónico de base de datos aplica un límite configurable para el tamaño de los datos adjuntos. Puede cambiar este límite usando el procedimiento almacenado [sysmail_configure_sp](/sql/relational-databases/system-stored-procedures/sysmail-configure-sp-transact-sql) .  
  
-   Extensiones de archivo prohibidas: el Correo electrónico de base de datos mantiene una lista de extensiones de archivo prohibidas. Los usuarios no pueden adjuntar archivos con las extensiones de la lista. Puede cambiar esta lista utilizando sysmail_configure_sp.  
  
-   Correo electrónico de base de datos se ejecuta bajo la cuenta de servicio de motor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para adjuntar un archivo de una carpeta a un mensaje de correo electrónico, la cuenta de motor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe tener permisos de acceso a la carpeta con el archivo.  
  
### <a name="supportability"></a>Compatibilidad  
  
-   Configuración integrada: el Correo electrónico de base de datos mantiene la información de las cuentas de correo electrónico de [!INCLUDE[ssDEnoversion](../../includes/tsql-md.md)].  
  
-   Registro. Correo electrónico de base de datos registra la actividad de correo electrónico en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en el registro de eventos de aplicación de Microsoft Windows y en las tablas de la base de datos **msdb** .  
  
-   Auditar: El Correo electrónico de base de datos conserva copias de los mensajes y datos adjuntos enviados en la base de datos **msdb** . Puede auditar fácilmente el uso del Correo electrónico de base de datos y revisar los mensajes conservados.  
  
-   Compatibilidad con HTML: el Correo electrónico de base de datos permite enviar mensajes de correo electrónico con el formato HTML.  
  

  
##  <a name="VisualElement"></a> Arquitectura del Correo electrónico de base de datos  
 El Correo electrónico de base de datos está diseñado en una arquitectura en cola que usa tecnologías de Service Broker. Cuando los usuarios ejecutan **sp_send_dbmail**, el procedimiento almacenado inserta un elemento en la cola de correo y crea un registro que contiene el mensaje de correo electrónico. La inserción de la nueva entrada en la cola de correo inicia el proceso externo de Correo electrónico de base de datos (DatabaseMail.exe). El proceso externo lee la información de correo electrónico y envía el mensaje de correo electrónico al servidor o servidores de correo electrónico adecuados. El proceso externo inserta un elemento en la cola Estado para el resultado de la operación de envío. La inserción de la nueva entrada en la cola de estado inicia el procedimiento almacenado interno que actualiza el estado del mensaje de correo electrónico. Además de almacenar el mensaje de correo electrónico enviado, o no enviado, el Correo electrónico de base de datos también registra cualquier dato adjunto del correo electrónico en las tablas del sistema. Las vistas del Correo electrónico de base de datos proporcionan el estado de los mensajes para solucionar problemas y los procedimientos almacenados permiten la administración de la cola del Correo electrónico de base de datos.  
  
 ![msdb envía mensajes a un servidor de correo SMTP](../../database-engine/media/databasemail.gif "msdb envía mensajes a un servidor de correo SMTP")  
  

  
##  <a name="ComponentsAndConcepts"></a> Introducción a los componentes de Correo electrónico de base de datos  
 El Correo electrónico de base de datos consta de los componentes principales siguientes:  
  
-   Componentes de seguridad y configuración  
  
     El Correo electrónico de base de datos almacena información de configuración y seguridad en la base de datos **msdb** . Los objetos de configuración y seguridad crean perfiles y cuentas usadas por el Correo electrónico de base de datos.  
  
-   Componentes de mensajería  
  
     La base de datos **msdb** actúa como la base de datos host de correo que contiene los objetos de mensajería que Correo electrónico de base de datos usa para enviar correo electrónico. Estos objetos incluyen el procedimiento almacenado **sp_send_dbmail** y las estructuras de datos que contienen información acerca de los mensajes.  
  
-   Ejecutable del Correo electrónico de base de datos  
  
     El ejecutable del Correo electrónico de base de datos es un programa externo que lee en una cola de la base de datos **msdb** y envía mensajes a servidores de correo electrónico.  
  
-   Componentes de registro y auditoría  
  
     El Correo electrónico de base de datos registra información de registro en la base de datos **msdb** y el registro de eventos de aplicación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Agente de configuración para usar el Correo electrónico de base de datos:**  
  
 El Agente SQL Server se puede configurar para usar el Correo electrónico de base de datos. Esto es necesario para la notificación de alertas y la notificación automática cuando se completa un trabajo.  
  
> [!WARNING]  
>  Cada paso de un trabajo puede también enviar un correo electrónico sin configurar el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar el Correo electrónico de la base de datos. Por ejemplo, un paso de trabajo de [!INCLUDE[tsql](../../../includes/tsql-md.md)] puede usar el Correo electrónico de base de datos para enviar el resultado de una consulta a la lista de destinatarios.  
  
 Puede configurar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para enviar mensajes de correo electrónico a operadores predefinidos cuando:  
  
-   Se desencadene una alerta. Las alertas se pueden configurar para enviar una notificación por correo electrónico acerca de eventos específicos que se produzcan. Por ejemplo, es posible configurar alertas para que avisen a un operador acerca de un determinado evento de la base de datos o una situación del sistema operativo que precise una acción inmediata. Para obtener más información sobre cómo configurar alertas, vea [Alertas](../../ssms/agent/alerts.md).  
  
-   Se lleve a cabo o no se complete una tarea programada, como una copia de seguridad de la base de datos o un evento de replicación. Por ejemplo, puede usar el correo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para notificar a los operadores si se produce un error durante el procesamiento a fin de mes.  
  
 
  
##  <a name="RelatedContent"></a> Temas de componentes del Correo electrónico de base de datos  
  
-   [Objetos de configuración de Correo electrónico de base de datos](database-mail-configuration-objects.md)  
  
-   [Objetos de mensajería de Correo electrónico de base de datos](database-mail-messaging-objects.md)  
  
-   [Programa externo Correo electrónico de base de datos](database-mail-external-program.md)  
  
-   [Registro y auditorías del Correo electrónico de base de datos](database-mail-log-and-audits.md)  
  
-   [Configurar el Agente SQL Server para que use el Correo electrónico de base de datos](configure-sql-server-agent-mail-to-use-database-mail.md)  
  

  
  
