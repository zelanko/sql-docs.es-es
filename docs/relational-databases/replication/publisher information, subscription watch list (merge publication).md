---
title: "Informaci&#243;n de publicador, Lista de supervisi&#243;n de suscripciones (Publicaci&#243;n de combinaci&#243;n, SQL Server 2005 y posteriores) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.monitor.publisherinfo.subscriptionssummary.merge.f1"
ms.assetid: 4ec956bf-5cef-4377-a1d1-8c7f0107a6cb
caps.latest.revision: 32
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Informaci&#243;n de publicador, Lista de supervisi&#243;n de suscripciones (Publicaci&#243;n de combinaci&#243;n, SQL Server 2005 y posteriores)
  La pestaña **Lista de supervisión de suscripciones** está disponible para distribuidores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores; está pensada para mostrar información sobre las suscripciones de todas las publicaciones disponibles en el publicador seleccionado. Puede filtrar la lista de suscripciones para ver errores, advertencias y las suscripciones que tienen un rendimiento bajo. Esta ficha proporciona una única ubicación para un administrador supervise toda la actividad de replicación en el publicador: Monitor de replicación muestra todas las suscripciones que requieren atención, basándose en el tipo de replicación seleccionada y en la opción elegida en el **Mostrar** cuadro de lista desplegable. Puesto que los elementos mostrados en esta pestaña se basan en el rendimiento y el estado actual, las suscripciones se muestran en esta página solo si coinciden con la opción del cuadro de lista **Mostrar** en el momento actual.  
  
## Opciones  
 Para obtener información más detallada y las tareas de una suscripción, haga clic con el botón secundario en la fila de dicha suscripción y, a continuación, haga clic en una opción del menú contextual. Para cambiar la manera que la cuadrícula muestra los datos, haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en una de las opciones siguientes:  
  
-   **Ordenar**: ordene en una o más columnas en el cuadro de diálogo **Ordenar columnas** .  
  
-   **Elegir columnas para mostrar**: seleccione las columnas que se mostrarán y el orden en el que se mostrarán en el cuadro de diálogo **Elegir columnas** .  
  
-   **Filtro**: filtre filas en la cuadrícula basándose en los valores de columna en el cuadro de diálogo **Configuración del filtro** .  
  
-   **Borrar filtro**: borre cualquier configuración de filtro para la cuadrícula.  
  
 La configuración del filtro es específica de cada cuadrícula. La selección y ordenación de las columnas se aplica a todas las cuadrículas del mismo tipo, como la cuadrícula de las publicaciones para cada Publicador.  
  
 **Mostrar suscripciones de mezcla**  
 Seleccione el tipo de suscripción (transaccional, de instantánea o de mezcla) que se mostrará para el publicador seleccionado.  
  
 **Mostrar**  
 Seleccione los estados de la suscripción que se mostrarán para el tipo de suscripción seleccionado. Por ejemplo, puede seleccionar mostrar solo aquellas suscripciones que tienen errores.  
  
 **Estado**  
 Estado de cada suscripción, que se determina mediante el estado del Agente de mezcla.  
  
 De forma predeterminada, la cuadrícula que contiene la información de suscripción se ordena por la **estado** columna (y, a continuación, ordenados por el **rendimiento** columna de las suscripciones con el mismo estado). La siguiente lista muestra los valores de estado posibles y el criterio de ordenación de los valores (por ejemplo, los errores se muestran siempre en la parte superior de la cuadrícula).  
  
-   Error  
  
-   Rendimiento crítico  
  
-   Mezcla de ejecución prolongada  
  
-   Con expiración en breve/Expirado  
  
-   Suscripción no inicializada  
  
-   Reintentando comando con errores  
  
-   Sincronizando  
  
-   No se están sincronizando  
  
 El criterio de clasificación también determina qué valor se muestra si una misma suscripción presenta varios estados. Por ejemplo, si una suscripción tiene un error y expirará en breve, la columna **Estado** muestra **Error**.  
  
 Los valores de estado **rendimiento crítico**, **mezcla de ejecución prolongada**, **expiración en breve/expirado**, y **suscripción no inicializada** son advertencias. Cuando se muestra una advertencia, también aparece la columna **Estado** si un agente está sincronizándose. Por ejemplo, el estado podría ser **Sincronizando, Rendimiento crítico**.  
  
 Los valores de estado **expiración en breve/expirado** y **mezcla de ejecución prolongada** se pueden mostrar sólo si se establecen umbrales. El valor de estado **rendimiento crítico** se pueden mostrar sólo después de cinco sincronizaciones de suscripciones con el mismo tipo de conexión (acceso telefónico o LAN). Para obtener información sobre las medidas de rendimiento y configuración de umbrales, consulte [Monitor de rendimiento con el Monitor de replicación](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) y [establecer umbrales y advertencias en el Monitor de replicación](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Suscripción**  
 El nombre de cada suscripción, con el formato:*Nombredesuscriptor: Nombredebasededatosdesuscripción*.  
  
 **Nombre descriptivo**  
 Descripción de cada suscripción. La descripción se introduce en la **Propiedades de suscripción** cuadro de diálogo o se especifica con el **@description** parámetro de [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) o [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Los usuarios normalmente usan la descripción como un "nombre descriptivo" o alias de la suscripción.  
  
 **Publicación**  
 El nombre de la publicación con la que se sincroniza una suscripción, en el formulario: *Nombredebasededatosdepublicación: Nombredepublicación*.  
  
 **Rendimiento**  
 Clasificación de rendimiento de cada suscripción, basada en las medidas más recientes de tasa de entrega obtenidas por el Monitor de replicación. La clasificación se determina comparando el rendimiento de una suscripción individual con el rendimiento medio histórico de las suscripciones a la publicación que tienen el mismo tipo de conexión (de acceso telefónico o LAN). El Monitor de replicación muestra un valor una vez que se han producido cinco sincronizaciones con al menos 50 cambios en cada una a través del mismo tipo de conexión. Si ha habido menos de cinco sincronizaciones con al menos 50 cambios, o la sincronización más reciente tiene menos de 50 cambios, está columna está en blanco.  
  
> [!NOTE]  
>  Rendimiento se basa en el tipo de conexión que se muestra en el **conexión** columna; por lo tanto, es posible que una suscripción con una tasa de entrega inferior para mostrar una mejor clasificación de rendimiento que otra suscripción si la primera suscripción se sincroniza mediante una conexión más lenta.  
  
 La clasificación de rendimiento tiene uno de los valores siguientes:  
  
-   Excelente  
  
-   Bueno  
  
-   Regular  
  
-   Insuficiente  
  
 Para obtener más información acerca de cómo se definen las evaluaciones de rendimiento y cómo se establecen los umbrales de rendimiento, consulte [Monitor de rendimiento con el Monitor de replicación](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Tasa de entrega**  
 Número de filas por segundo procesadas por el Agente de mezcla.  
  
 **Última sincronización**  
 Hora en que se ejecutó el Agente de mezcla por última vez. Durante esta sincronización se pueden procesar o no procesar los cambios. Si la sincronización está en curso, se muestra un valor de porcentaje de finalización.  
  
 **Duración**  
 Tiempo durante el que se ha estado ejecutando el Agente de mezcla en la última sincronización. El tiempo representa el tiempo transcurrido si el Agente de mezcla se está sincronizando actualmente y el tiempo total si el Agente de mezcla se ha sincronizado con anterioridad.  
  
 **Conexión**  
 Tipo de conexión entre el suscriptor y el publicador. Los valores posibles son **LAN**, **Acceso telefónico**e **Internet**. Si la suscripción utiliza sincronización web, se muestra el valor **Internet** .  
  
## Vea también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Ver la información y realizar tareas para un publicador & #40; Monitor de replicación & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [Sincronización web para la replicación de mezcla](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  