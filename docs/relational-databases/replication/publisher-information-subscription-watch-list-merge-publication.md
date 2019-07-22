---
title: Información de publicador, Lista de supervisión de suscripciones (Publicación de combinación) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.publisherinfo.subscriptionssummary.merge.f1
ms.assetid: 4ec956bf-5cef-4377-a1d1-8c7f0107a6cb
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: dca1dfc281ac4ea63c2c28b35dc93805f2c19b2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021401"
---
# <a name="publisher-information-subscription-watch-list-merge-publication"></a>Información de publicador, Lista de supervisión de suscripciones (Publicación de combinación)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La pestaña **Lista de supervisión de suscripciones** está disponible para distribuidores que ejecutan [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores; está pensada para mostrar información sobre las suscripciones de todas las publicaciones disponibles en el publicador seleccionado. Puede filtrar la lista de suscripciones para ver errores, advertencias y las suscripciones que tienen un rendimiento bajo. En esta pestaña se proporciona una ubicación única para que un administrador supervise toda la actividad de replicación en un publicador: en el Monitor de replicación se muestran todas las suscripciones que necesitan atención, en función del tipo de replicación seleccionado y de la opción elegida en el cuadro de lista desplegable **Mostrar**. Puesto que los elementos mostrados en esta pestaña se basan en el rendimiento y el estado actual, las suscripciones se muestran en esta página solo si coinciden con la opción del cuadro de lista **Mostrar** en el momento actual.  
  
## <a name="options"></a>Opciones  
 Para obtener información más detallada y las tareas de una suscripción, haga clic con el botón secundario en la fila de dicha suscripción y, a continuación, haga clic en una opción del menú contextual. Para cambiar la manera que la cuadrícula muestra los datos, haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en una de las opciones siguientes:  
  
-   **Ordenar**: ordene por una o más columnas en el cuadro de diálogo **Ordenar columnas**.  
  
-   **Elegir columnas para mostrar**: seleccione las columnas que se van a mostrar y el orden en el que lo harán en el cuadro de diálogo **Elegir columnas**.  
  
-   **Filtro**: filtre las filas de la cuadrícula en función de los valores de columna del cuadro de diálogo **Configuración del filtro**.  
  
-   **Borrar filtro**: borre cualquier configuración de filtro para la cuadrícula.  
  
 La configuración del filtro es específica de cada cuadrícula. La selección y ordenación de las columnas se aplica a todas las cuadrículas del mismo tipo, como la cuadrícula de las publicaciones para cada Publicador.  
  
 **Mostrar suscripciones de mezcla**  
 Seleccione el tipo de suscripción (transaccional, de instantánea o de mezcla) que se mostrará para el publicador seleccionado.  
  
 **Mostrar**  
 Seleccione los estados de la suscripción que se mostrarán para el tipo de suscripción seleccionado. Por ejemplo, puede seleccionar mostrar solo aquellas suscripciones que tienen errores.  
  
 **Estado**  
 Estado de cada suscripción, que se determina mediante el estado del Agente de mezcla.  
  
 De forma predeterminada, la cuadrícula que contiene la información de suscripción está ordenada por la columna **Estado** (y, a continuación, por la columna **Rendimiento** de las suscripciones con el mismo estado). La siguiente lista muestra los valores de estado posibles y el criterio de ordenación de los valores (por ejemplo, los errores se muestran siempre en la parte superior de la cuadrícula).  
  
-   Error  
  
-   Rendimiento crítico  
  
-   Mezcla de ejecución prolongada  
  
-   Con expiración en breve/Expirada  
  
-   Suscripción no inicializada  
  
-   Reintentando comando con errores  
  
-   Sincronizando  
  
-   No se están sincronizando  
  
 El criterio de clasificación también determina qué valor se muestra si una misma suscripción presenta varios estados. Por ejemplo, si una suscripción tiene un error y expirará en breve, la columna **Estado** muestra **Error**.  
  
 Los valores de estado **Rendimiento crítico**, **Mezcla de ejecución prolongada**, **Con expiración en breve/Expirado**y **Suscripción no inicializada** son advertencias. Cuando se muestra una advertencia, también aparece la columna **Estado** si un agente está sincronizándose. Por ejemplo, el estado podría ser **Sincronizando, Rendimiento crítico**.  
  
 Los valores de estado **Con expiración en breve/Expirado** y **Mezcla de ejecución prolongada** solo se pueden mostrar si se han establecido umbrales. El valor de estado **Rendimiento crítico** solamente se puede mostrar después de realizar cinco sincronizaciones de suscripciones con el mismo tipo de conexión (acceso telefónico o LAN). Para obtener información sobre la medición del rendimiento y el establecimiento de umbrales, vea [Supervisar el rendimiento con el Monitor de replicación](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md) y [Establecer umbrales y advertencias en el Monitor de replicación](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md).  
  
 **Suscripción**  
 Nombre de cada suscripción, con el formato: *NombreDeSuscriptor: NombreDeBaseDeDatosDeSuscripción*.  
  
 **Nombre descriptivo**  
 Descripción de cada suscripción. La descripción se escribe en el cuadro de diálogo **Propiedades de suscripción** o se especifica con el parámetro **@description** de [sp_addmergesubscription](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md) o [sp_addmergepullsubscription](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md). Los usuarios normalmente usan la descripción como un "nombre descriptivo" o alias de la suscripción.  
  
 **Publicación**  
 El nombre de la publicación con la que se sincroniza una suscripción, en el formato: *NombreDeBaseDeDatosDePublicación: nombreDePublicación*.  
  
 **Rendimiento**  
 Clasificación de rendimiento de cada suscripción, basada en las medidas más recientes de tasa de entrega obtenidas por el Monitor de replicación. La clasificación se determina comparando el rendimiento de una suscripción individual con el rendimiento medio histórico de las suscripciones a la publicación que tienen el mismo tipo de conexión (de acceso telefónico o LAN). El Monitor de replicación muestra un valor una vez que se han producido cinco sincronizaciones con al menos 50 cambios en cada una a través del mismo tipo de conexión. Si ha habido menos de cinco sincronizaciones con al menos 50 cambios, o la sincronización más reciente tiene menos de 50 cambios, está columna está en blanco.  
  
> [!NOTE]  
>  El rendimiento se basa en el tipo de conexión que se muestra en la columna **Conexión** ; por tanto, es posible que una suscripción con una tasa de entrega menor muestre una mejor clasificación de rendimiento que otra suscripción si la primera se ha sincronizado en una conexión más lenta.  
  
 La clasificación de rendimiento tiene uno de los valores siguientes:  
  
-   Excelente  
  
-   Bueno  
  
-   Regular  
  
-   Insuficiente  
  
 Para obtener más información sobre cómo se definen las clasificaciones de rendimiento y cómo se establecen los umbrales de rendimiento, vea [Supervisar el rendimiento con el Monitor de replicación](../../relational-databases/replication/monitor/monitor-performance-with-replication-monitor.md).  
  
 **Tasa de entrega**  
 Número de filas por segundo procesadas por el Agente de mezcla.  
  
 **Última sincronización**  
 Hora en que se ejecutó el Agente de mezcla por última vez. Durante esta sincronización se pueden procesar o no procesar los cambios. Si la sincronización está en curso, se muestra un valor de porcentaje de finalización.  
  
 **Duración**  
 Tiempo durante el que se ha estado ejecutando el Agente de mezcla en la última sincronización. El tiempo representa el tiempo transcurrido si el Agente de mezcla se está sincronizando actualmente y el tiempo total si el Agente de mezcla se ha sincronizado con anterioridad.  
  
 **Conexión**  
 Tipo de conexión entre el suscriptor y el publicador. Los valores posibles son **LAN**, **Acceso telefónico**e **Internet**. Si la suscripción utiliza sincronización web, se muestra el valor **Internet** .  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Ver información y realizar tareas para un publicador &#40;Monitor de replicación&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication.md)  (Supervisar la replicación)  
 [Sincronización web para la replicación de mezcla](../../relational-databases/replication/web-synchronization-for-merge-replication.md)  
  
  
