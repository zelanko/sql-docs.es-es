---
title: Programaciones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- schedules [Reporting Services]
- schedules [Reporting Services], about schedules
- published reports [Reporting Services], schedules
- reports [Reporting Services], scheduling
- subscriptions [Reporting Services], scheduling
- automatic report processing
ms.assetid: ecccd16b-eba9-4e95-b55d-f15c621e003f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 69acb3d6495ce7ec77b67feed7644945a477a86e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62654411"
---
# <a name="schedules"></a>Programaciones
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona programaciones compartidas y programaciones específicas del informe para ayudarle a controlar el procesamiento y distribución de los informes. La diferencia entre los dos tipos de programaciones radica en cómo se definen, almacenan y administran. La construcción interna de los dos tipos de programación es la misma. Todas las programaciones especifican un tipo de periodicidad: mensual, semanal o diaria. Dentro del tipo de periodicidad, se deben establecer los intervalos y el período para la frecuencia con que se debe producir un evento. El tipo de patrón de periodicidad y cómo se especifican los patrones es el mismo si crea una programación compartida o una programación específica del informe.  
  
 En este tema:  
  
-   [Lo que puede hacer con las programaciones](#bkmk_whatyoucando)  
  
-   [Comparar programaciones compartidas y específicas del informe](#bkmk_compare)  
  
-   [Configurar los orígenes de datos](#bkmk_configuredatasources)  
  
-   [Store credenciales y cuentas de procesamiento](#bkmk_credentials)  
  
-   [Programación y funcionamiento del procesador de entrega](#bkmk_how_scheduling_works)  
  
-   [Dependencias de servidor](#bkmk_serverdependencies)  
  
-   [Efectos de detener al Agente SQL Server](#bkmk_stoppingagent)  
  
-   [Efectos de detener el servicio del servidor de informes](#bkmk_stoppingservice)  
  
  
##  <a name="bkmk_whatyoucando"></a> Qué puede hacer con las programaciones  
 Puede usar el Administrador de informes en modo nativo y las páginas de administración de sitios de SharePoint en modo de SharePoint para crear y administrar programaciones. Puede hacer lo siguiente:  
  
-   Programar la entrega del informe mediante una suscripción estándar o controlada por datos.  
  
-   Programar el historial del informe de modo que se agreguen instantáneas nuevas a él a intervalos regulares.  
  
-   Programar el momento de actualización de los datos de una instantánea de informe.  
  
-   Programar cuándo actualizar los datos de un conjunto de datos compartido  
  
-   Programar la expiración de un informe en caché o conjunto de datos compartidos para que tenga lugar a una hora predefinida a fin de poder actualizarlo posteriormente.  
  
 Puede crear una programación compartida si desea utilizar la misma información de programación para varios informes o suscripciones. Las programaciones compartidas se definen aparte y, posteriormente, se hace referencia a ellas en los informes, conjuntos de datos compartidos y suscripciones que precisan información sobre la programación.  
  
 Cuando se crea una programación, el informe guarda la información de programación en la base de datos del servidor de informes o para el modo de SharePoint, en la base de datos de aplicación de servicio. El servidor de informes también crea un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se usa para desencadenar la programación. El procesamiento de programaciones se basa en la hora local del servidor de informes que contiene la programación. El formato de hora sigue el estándar del sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Para obtener información detallada acerca de cómo crear y administrar programaciones, vea [Create, Modify, and Delete Schedules](create-modify-and-delete-schedules.md).  
  
> [!NOTE]  
>  Las operaciones de programación no están disponibles en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Características compatibles con las ediciones de SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (https://go.microsoft.com/fwlink/?linkid=232473).  
  
##  <a name="bkmk_compare"></a> Comparar programaciones compartidas y programaciones específicas del informe  
 Ambos tipos de programaciones producen el mismo resultado:.  
  
-   Las**programaciones compartidas** son elementos multipropósito, que se pueden trasladar y que contienen información de programación lista para usar. Dado que las programaciones compartidas son elementos de nivel de sistema, crear una programación de este tipo requiere permisos de nivel de sistema. Por este motivo, un administrador de un servidor de informes o un administrador de contenido suele crear las programaciones compartidas disponibles en el servidor de informes. Las programaciones compartidas se almacenan y administran en el servidor de informes mediante el Administrador de informes o la configuración de sitio de SharePoint.  
  
     A diferencia de las programaciones específicas que defina a través de las propiedades de informe, conjunto de datos compartidos o suscripciones, las programaciones compartidas son más fáciles de administrar y mantener por los siguientes motivos:  
  
    -   Las programaciones compartidas se pueden administrar desde una ubicación central, facilitando la comparación de las propiedades de programación y el ajuste de los patrones de periodicidad y frecuencia si se ejecutan operaciones programadas demasiado seguidas o que están en conflicto con otros procesos del servidor.  
  
    -   Permiten adaptarse rápidamente a los cambios del entorno informático. Por ejemplo, suponga que tiene un conjunto de informes que se ejecutan a las 4:00 a.m. después de que se actualice un almacenamiento de datos. Si la operación de actualización de datos se vuelve a programar o se retrasa, puede adaptar con facilidad dicho cambio actualizando la información de programación en una programación compartida única.  
  
    -   Si solo usa programaciones compartidas, sabrá de forma precisa cuándo se producen las operaciones programadas. Esto hace más sencillo preveer y ajustar las cargas del servidor antes de que se produzcan problemas de rendimiento. Por ejemplo, si decide programar copias de seguridad del equipo a una hora concreta, puede ajustar las programaciones compartidas para que se ejecuten en momentos diferentes.  
  
-   Las**programaciones específicas del informe** se definen en el contexto de un informe individual, suscripción u operación de ejecución de informes para determinar las actualizaciones de la expiración de la memoria caché o de la instantánea. Estas programaciones se insertan durante la definición de una suscripción o el establecimiento de las propiedades de ejecución del informe. Las programaciones específicas del informe se pueden crear cuando la programación compartida no ofrece el modelo de frecuencia o periodicidad deseado. Para evitar que se ejecute un informe, las programaciones específicas del informe deben modificarse manualmente. Las programaciones específicas del informe las crean los usuarios individuales.  
  
##  <a name="bkmk_configuredatasources"></a> Configurar los orígenes de datos  
 Para poder programar el procesamiento de una suscripción o datos para un informe, debe configurar el origen de datos del informe para usar las credenciales almacenadas o la cuenta de procesamiento de informes desatendido. Si usa credenciales almacenadas, solo puede almacenar un conjunto de credenciales, que usarán todos los usuarios que ejecuten el informe. Las credenciales pueden ser una cuenta de usuario de Windows o una cuenta de usuario de base de datos.  
  
 La cuenta de procesamiento de informes desatendido es una cuenta especial configurada en el servidor de informes. El servidor de informes la usa para conectarse a equipos remotos cuando una operación programada requiere la recuperación de un procesamiento o archivo externo. Si configura la cuenta, puede usarla para conectarse a los orígenes de datos externos que proporcionan datos a un informe.  
  
 Para especificar las credenciales almacenadas o la cuenta de procesamiento de informes desatendido, modifique las propiedades del origen de datos del informe. En lugar de ello, si el informe usa un origen de datos compartido, modifíquelo.  
  
##  <a name="bkmk_credentials"></a> Almacenar credenciales y cuentas de procesamiento  
 El modo que adopte para trabajar con las programaciones dependerá de las tareas de su asignación de roles. Si usa roles predefinidos, los usuarios que son administradores de contenido y administradores del sistema pueden crear y administrar cualquier programación. Si utiliza asignaciones de roles personalizados, deberán incluir tareas compatibles con operaciones programadas.  
  
|Para|Incluya estas tareas|Roles predefinidos en modo nativo|Grupos en modo de SharePoint|  
|----------------|-----------------------|----------------------------------|----------------------------|  
|Crear, modificar o eliminar programaciones compartidas|Administrar programaciones compartidas|Administrador del sistema|Propietarios|  
|Seleccionar programaciones compartidas|Ver programaciones compartidas|Usuario del sistema|Miembros|  
|Crear, modificar o eliminar programaciones específicas del informe en una suscripción definida por el usuario|Administrar suscripciones individuales|Explorador, Generador de informes, Mis informes, Administrador de contenido|Visitantes, Miembros|  
|Crear, modificar o eliminar programaciones específicas del informe para todo el resto de operaciones programadas|Administrar historial de informe, Administrar todas las suscripciones y Administrar informes|Administrador de contenido|Propietarios|  
  
 Para más información sobre la seguridad en un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]en modo nativo, vea [Roles predefinidos](../security/role-definitions-predefined-roles.md), [Conceder permisos en un servidor de informes en modo nativo](../security/granting-permissions-on-a-native-mode-report-server.md) y [Tareas y permisos](../security/tasks-and-permissions.md). Para el modo de SharePoint, vea [Comparación de roles y tareas en Reporting Services con grupos y permisos de SharePoint](../reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md)  
  
##  <a name="bkmk_how_scheduling_works"></a> Funcionamiento del Procesador de entrega y programación  
 El Procesador de entrega y programación ofrece las siguientes funcionalidades:  
  
-   Mantiene una cola de eventos y notificaciones en la base de datos del servidor de informes. En una implementación escalada, la cola se comparte en todos los servidores de informes de la implementación.  
  
-   Llama al Procesador de informes para ejecutar informes, procesar suscripciones o borrar informes de la memoria caché. Todo el procesamiento de informes que se produce como consecuencia de un evento de programación se realiza como un proceso en segundo plano. El modo de SharePoint usa trabajos de temporizador para .  
  
-   Llama a la extensión de entrega especificada en una suscripción para que el informe se pueda entregar.  
  
 Otros componentes y servicios que funcionan con el Procesador de entrega y programación controlan otros aspectos de la operación de programación y entrega. En concreto, el Procesador de entrega y programación se ejecuta en el servicio del servidor de informes y utiliza el Agente SQL Server como temporizador para generar eventos programados. En la descripción paso a paso siguiente se explica el funcionamiento de las operaciones programadas en una implementación de Reporting Services:  
  
1.  Las operaciones programadas se definen cuando un usuario crea una programación. En la programación se definen la fecha y hora en que se desencadenará una suscripción para la entrega de informes, se actualizará una instantánea o expirará una memoria caché.  
  
2.  El servidor de informes guarda la información de programación en su base de datos.  
  
3.  El servidor de informes crea un trabajo correspondiente en el Agente SQL Server que contiene la información de programación facilitada. Los trabajos se crean gracias a un procedimiento almacenado, mediante la conexión abierta existente con la base de datos del servidor de informes.  
  
4.  El Agente SQL Server ejecuta el trabajo en la fecha y hora especificadas en la programación. El trabajo crea un evento que se agrega a una cola que mantiene Reporting Services.  
  
5.  El evento hace que se produzca un proceso de informe o suscripción. Los eventos se procesan cuando son detectados en la cola; el informe se procesa o entrega en consecuencia.  
  
     Antes de que se procesen los eventos, el Procesador de entrega y programación realiza un paso de autenticación para comprobar que el propietario de la suscripción tiene permiso para ver el informe.  
  
 Reporting Services mantiene una cola de eventos para todas las operaciones programadas. La sondea a intervalos regulares para detectar nuevos eventos. De forma predeterminada, la cola se recorre a intervalos de 10 segundos. Es posible cambiar el intervalo si se modifican los valores de configuración `PollingInterval`, `IsNotificationService` e `IsEventService` del archivo RSReportServer.config. El modo de SharePoint también usa el archivo RSreporserver.config para estas configuraciones y los valores se aplican a todas las aplicaciones de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para más información, consulte [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md).  
  
##  <a name="bkmk_serverdependencies"></a> Dependencias de servidor  
 El Procesador de entrega y programación requiere que se hayan iniciado el servicio del servidor de informes y el Agente SQL Server. La característica procesador de entrega y programación debe habilitarse a través de la `ScheduleEventsAndReportDeliveryEnabled` propiedad de la **configuración de área expuesta para Reporting Services** faceta de administración basada en directivas. Tanto el Agente SQL Server como el servicio del servidor de informes deben estar en ejecución para que se puedan realizar las operaciones programadas.  
  
> [!NOTE]  
>  Se puede utilizar la faceta **Configuración de área expuesta para Reporting Services** con el fin de detener las operaciones programadas de manera temporal o permanente. Aunque puede crear e implementar extensiones de entrega personalizadas, el Procesador de entrega y programación en sí mismo no es extensible. No se puede cambiar el modo en que administra eventos y notificaciones. Para obtener más información acerca de cómo desactivar características, vea la sección **Eventos programados y entrega programada** de [Turn Reporting Services Features On or Off](../report-server/turn-reporting-services-features-on-or-off.md).  
  
###  <a name="bkmk_stoppingagent"></a> Efectos de detener el Agente SQL Server  
 Para procesar informes programados, se utiliza de forma predeterminada el Agente SQL Server. Si se detiene el servicio, las nuevas solicitudes de procesamiento solo se pueden agregar a la cola mediante programación con el método <xref:ReportService2010.ReportingService2010.FireEvent%2A> . Cuando se reinicia el servicio, se reanudan los trabajos que crean solicitudes de procesamiento de informes. El servidor de informes no trata de volver a crear trabajos de procesamiento de informes que pudieran haberse producido en el pasado, mientras el Agente SQL Server estaba sin conexión. Si se detiene el Agente SQL Server durante una semana, todas las operaciones programadas se pierden para esa semana.  
  
> [!NOTE]  
>  Las funciones que proporciona el Agente SQL Server a Reporting Services se pueden reemplazar con código personalizado que use el método <xref:ReportService2010.ReportingService2010.FireEvent%2A> para agregar eventos de programación a la cola.  
  
###  <a name="bkmk_stoppingservice"></a> Efectos de detener el servicio del servidor de informes  
 Si se detiene el servicio del servidor de informes, el Agente SQL Server sigue agregando solicitudes de procesamiento de informes a la cola. La información de estado del Agente SQL Server indica que el trabajo concluyó correctamente. No obstante, puesto que se ha detenido el servicio del servidor de informes, en realidad no se produce el procesamiento de informes. Las solicitudes se siguen acumulando en la cola hasta que se reinicia el servicio del servidor de informes. Una vez reiniciado este servicio, todas las solicitudes de procesamiento de informes existentes en la cola se procesan por orden.  
  
## <a name="see-also"></a>Vea también  
 [Crear, modificar y eliminar instantáneas del historial de informes](../report-server/create-modify-and-delete-snapshots-in-report-history.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions-and-delivery-reporting-services.md)   
 [Data-Driven Subscriptions](data-driven-subscriptions.md)   
 [Informes almacenados en caché &#40;SSRS&#41;](../report-server/caching-reports-ssrs.md)   
 [Administración de contenido del servidor de informes &#40;Modo nativo de SSRS&#41;](../report-server/report-server-content-management-ssrs-native-mode.md)   
 [Almacenar en caché conjuntos de datos compartidos &#40;SSRS&#41;](../report-server/cache-shared-datasets-ssrs.md)  
  
  
