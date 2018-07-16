---
title: Instancias del motor de base de datos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: af9ae643-9866-4014-b36f-11ab556a773e
caps.latest.revision: 15
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 243524a0f073ab1950398eff715bd1f1420144a3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37291351"
---
# <a name="database-engine-instances-sql-server"></a>Instancias del motor de base de datos (SQL Server)
  Una instancia de la [!INCLUDE[ssDE](../../includes/ssde-md.md)] es una copia de la `sqlservr.exe` ejecutable que se ejecuta como un servicio de sistema operativo. Cada instancia administra varias bases de datos del sistema y una o varias bases de datos de usuario. Cada equipo puede ejecutar varias instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Las aplicaciones se conectan a la instancia para realizar el trabajo en una base de datos administrada por la instancia.  
  
## <a name="instances"></a>Instancias  
 Una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] funciona como un servicio que controla todas las solicitudes de aplicación para trabajar con datos de cualquiera de las bases de datos administradas por dicha instancia. Es el destino de las solicitudes de conexión (inicios de sesión) de aplicaciones. La conexión se ejecuta en una conexión de red si la aplicación y la instancia están en equipos independientes. Si la aplicación y la instancia están en el mismo equipo, la conexión de SQL Server se puede ejecutar como una conexión de red o una conexión en memoria. Cuando una conexión se ha completado, una aplicación envía instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] a través de la conexión hasta la instancia. La instancia resuelve las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] en operaciones con los datos y objetos de las bases de datos y, si se han concedido los permisos necesarios a las credenciales de inicio de sesión, realiza el trabajo. Los datos recuperados se devuelven a la aplicación, junto con cualesquiera mensajes como errores.  
  
 Puede ejecutar múltiples instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)] en un equipo. Una instancia puede ser la instancia predeterminada. La instancia predeterminada no tiene nombre. Si una solicitud de conexión especifica solo el nombre del equipo, se establece la conexión a la instancia predeterminada. Una instancia con nombre es una instancia en la que se especifica un nombre de instancia al instalar la instancia. Una solicitud de conexión debe especificar el nombre del equipo y el nombre de instancia para conectar a la instancia. No hay ningún requisito para instalar una instancia predeterminada; todas las instancias que se ejecutan en un equipo pueden ser instancias con nombre.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo configurar las propiedades de una instancia. Configure los valores predeterminados como ubicaciones de archivos y formatos de fecha, o cómo la instancia usa los recursos del sistema operativo, como la memoria o los subprocesos.|[Configurar instancias del motor de base de datos &#40;SQL Server&#41;](database-engine-instances-sql-server.md)|  
|Describe cómo administrar intercalación de una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Las intercalaciones definen los patrones de bits que se usan para representar caracteres, y los comportamientos asociados como ordenación y operaciones de comparación de casos o de distinción de acentos.|[Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)|  
|Describe cómo configurar las definiciones de servidores vinculados, que permiten que las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] se ejecutan en una instancia para trabajar con los datos almacenados en orígenes de datos OLE DB independientes.|[Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)|  
|Describe cómo crear un desencadenador de inició de sesión, que especifica acciones que deben llevarse a cabo una vez que se haya validado un inició de sesión, pero antes de empiece a trabajar con los recursos de la instancia. Los desencadenadores de inició de sesión admiten acciones como la actividad de conexión del registro, o limitar los inicios de sesión basadas en la lógica y en la autenticación de credenciales realizada por Windows y SQL Server.|[Desencadenadores logon](../../relational-databases/triggers/logon-triggers.md)|  
|Describe cómo administrar el servicio asociado a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Esto incluye acciones como iniciar y detener el servicio o configurar opciones de inicio de acciones como iniciar y detener el servicio u opciones de configuración de opciones de inicio.|[Administrar el servicio del motor de base de datos](manage-the-database-engine-services.md)|  
|Describe la forma de realizar tareas de configuración de red del servidor tales como habilitar protocolos, modificar el puerto o la canalización usados por el protocolo, configurar el cifrado, configurar el servicio SQL Server Browser, exponer u ocultar el motor de base de datos de SQL Server en la red y registrar el nombre de la entidad de seguridad del servidor.|[Configuración de red del servidor](server-network-configuration.md)|  
|Describe cómo realizar tareas de configuración de red de cliente tales como configurar protocolos de cliente y crear o eliminar un alias de servidor.|[Configuración de red de cliente](client-network-configuration.md)|  
|Describe los editores de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] que se pueden usar para diseñar, depurar y ejecutar scripts como scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] . También describe cómo codificar scripts de Windows PowerShell para trabajar con componentes de SQL Server.|[Scripting del motor de base de datos](../../relational-databases/scripting/database-engine-scripting.md)|  
|Describe cómo usar planes de mantenimiento para especificar un flujo de trabajo de tareas habituales de administración de una instancia. Los flujos de trabajo incluyen tareas como hacer copias de seguridad de bases de datos y actualizar las estadísticas para mejorar el rendimiento.|[Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)|  
|Describe cómo usar el regulador de recursos para administrar el consumo de recursos y las cargas de trabajo especificando los límites de CPU y de memoria que las solicitudes de aplicación pueden usar.|[Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)|  
|Describe cómo las aplicaciones de base de datos pueden usar el correo electrónico de base de datos para enviar mensajes de correo electrónico desde [!INCLUDE[ssDE](../../includes/ssde-md.md)].|[Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md)|  
|Describe cómo el uso de eventos extendidos para capturar datos de rendimiento se puede usar para compilar líneas base de rendimiento o para diagnosticar problemas de rendimiento. Los eventos extendidos son un sistema ligero con un alto nivel de escalabilidad para recopilar datos de rendimiento.|[Eventos extendidos](../../relational-databases/extended-events/extended-events.md)|  
|Describe cómo usar el seguimiento de SQL para compilar un sistema personalizado de captura y registro de eventos en [!INCLUDE[ssDE](../../includes/ssde-md.md)].|[Seguimiento de SQL](../../relational-databases/sql-trace/sql-trace.md)|  
|Describe cómo usar el generador de perfiles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para capturar el seguimiento de solicitudes de aplicación que entran en una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Los seguimientos se pueden reproducir posteriormente para actividades como pruebas de rendimiento o diagnóstico de problemas.|[SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)|  
|Describe la captura de datos modificados (CDC) y las características de seguimiento de cambios y cómo se usan estas características para realizar el seguimiento de cambios en los datos de una base de datos.|[Seguimiento de cambios de datos &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)|  
|Describe cómo usar el visor del archivo de registro para buscar y ver los errores y mensajes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en diversos registros; por ejemplo el historial de trabajos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los registros de SQL Server y los registros de eventos de Windows.|[Visor de archivos de registro](../../relational-databases/logs/log-file-viewer.md)|  
|Describe cómo usar el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para analizar las bases de datos y hacer recomendaciones para tratar problemas potenciales de rendimiento.|[Asistente para la optimización de motor de base de datos](../../relational-databases/performance/database-engine-tuning-advisor.md)|  
|Describe cómo los administradores de base de datos de producción pueden establecer una conexión de diagnóstico a instancias cuando las conexiones estándar no se están aceptando.|[Conexión de diagnóstico para administradores de bases de datos](diagnostic-connection-for-database-administrators.md)|  
|Describe cómo usar la característica desusada de servidores remotos para habilitar el acceso desde una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] a otra. El mecanismo preferido para esta funcionalidad es un servidor vinculado.|[Servidores remotos](remote-servers.md)|  
|Describe las capacidades de Service Broker para las aplicaciones de mensajería y de puesta en cola, y proporciona punteros a la documentación de Service Broker.|[Service Broker](sql-server-service-broker.md)|  
|Describe cómo se puede utilizar la extensión del grupo de búferes para proporcionar una integración sin problemas del almacenamiento de acceso aleatorio no volátil (unidades de estado sólido) con el grupo de búferes del motor de base de datos para mejorar significativamente el rendimiento de E/S.|[Archivo de la extensión del grupo de búferes](buffer-pool-extension.md)|  
  
## <a name="see-also"></a>Vea también  
 [sqlservr (aplicación)](../../tools/sqlservr-application.md)   
 [Características de la base de datos](../../relational-databases/database-features.md)   
 [Características entre instancias del motor de base de datos](../database-engine-cross-instance-features.md)  
  
  
