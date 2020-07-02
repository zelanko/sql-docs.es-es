---
title: Supervisar las actividades de DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.administration.activitymonitoring.f1
helpviewer_keywords:
- monitoring activity
- activity monitoring
ms.assetid: 1d4c76f3-0d7b-498e-b792-4db4a0349814
author: swinarko
ms.author: sawinark
ms.openlocfilehash: ba2bfe0a9979d94df43b923b7eff2ed68750e19a
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85809974"
---
# <a name="monitor-dqs-activities"></a>Supervisar las actividades de DQS

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  En este tema se describe cómo supervisar de forma centralizada las actividades siguientes en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS): detección de conocimiento, administración de dominios, directiva de coincidencia, limpieza de datos, coincidencia de datos y limpieza SSIS.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 Solo los usuarios que dispongan del rol dqs_administrator en la base de datos DQS_Main pueden terminar una actividad o detener un proceso dentro de una actividad.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
  
-   Debe disponer del rol dqs_kb_editor o dqs_kb_operator en la base de datos DQS_MAIN para ver las actividades de DQS.  
  
-   Debe disponer del rol dqs_administrator en la base de datos DQS_MAIN para terminar una actividad o detener un proceso dentro de una actividad, además de para ver las actividades de DQS.  
  
##  <a name="view-dqs-activities"></a><a name="View"></a> Ver las actividades de DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Supervisión de actividades**. Aparece la pantalla de supervisión de actividades.  
  
     ![Pantalla Supervisión de actividades](../data-quality-services/media/dqs-activitymonitoring.gif "Pantalla Supervisión de actividades")  
  
3.  La pantalla de supervisión de actividades muestra información sobre cada actividad en una cuadrícula de actividades. La cuadrícula de actividades muestra la información siguiente sobre cada actividad de DQS:  
  
     **ID**: un valor entero. Número de actividad único generado por el sistema para la supervisión de la actividad.  
  
     **Name**: el nombre de la base de conocimientos o del proyecto de calidad de datos que se utiliza para esta actividad.  
  
     **Is Active**: indica si la actividad está activa o no. Puede presentar los siguientes valores:  
  
    -   **Activa**: la actividad se está ejecutando actualmente.  
  
    -   **Finalizada**: la actividad ha finalizado.  
  
    -   **Terminada**: la actividad la ha dado por terminada el administrador de DQS mediante la pantalla de supervisión de actividades o la ha cancelado el usuario mientras se ejecutaba en el área de características correspondiente en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].  
  
     **Type**: indica el tipo de actividad. **Sub Type** : indica el flujo de trabajo específico que se ejecuta para un tipo de actividad. Se supervisan los siguientes tipos de actividades:  
  
    -   Subtipos de**administración del conocimiento** :  
  
        -   **Detección de conocimiento**  
  
        -   **Administración de dominios**  
  
        -   **Directiva de coincidencia**  
  
    -   Subtipos de**proyecto DQ** :  
  
        -   **Limpieza**  
  
        -   **Coincidencia**  
  
    -   Subtipo de**limpieza SSIS** :  
  
        -   **Limpieza**  
  
     **Estado actual**: indica el estado actual de una actividad. El último proceso de cálculo determina el estado de la actividad. Tenga en cuenta que puede haber varios procesos de cálculo en una actividad, como ejecutar el proceso de detección varias veces (dentro de la actividad de detección de conocimiento). Por consiguiente, el estado puede cambiar varias veces durante la duración de la actividad.  
  
     **Estado actual** puede tener los valores siguientes:  
  
    -   **En ejecución**: el proceso de cálculo se está ejecutando.  
  
    -   **Correcto**: este estado se establece antes de que un proceso de cálculo se ha ejecutado y nuevamente después de que un proceso de cálculo finaliza correctamente.  
  
    -   **Error**: el proceso de cálculo no se ha realizado correctamente.  
  
    -   **Detenido**: el proceso de cálculo se detuvo.  
  
     **DQKB**: nombre de la base de conocimientos que se usa para la actividad.  
  
     **Usuario**: el nombre del usuario que inició actividad, o el último usuario que trabajó en la actividad (en caso de que no coincidan).  
  
     **Hora de inicio de la actividad**: la fecha y hora en que se inició la actividad.  
  
     **Tiempo transcurrido**: el tiempo transcurrido desde que se inició la actividad. Se muestra con el formato HH:MM:SS.  
  
     **Hora de finalización de la actividad**: la fecha y hora en que finalizó la actividad.  
  
##  <a name="filter-dqs-activity-information"></a><a name="Filter"></a> Filtrar la información de las actividades de DQS  
 Puede utilizar el panel de filtrado (**Filtrar por**, **Valor**, **Desde la fecha**y **Hasta la fecha**) en la pantalla de supervisión de actividades para filtrar y ver las actividades requeridas basándose en un determinado criterio de filtrado. Para filtrar los registros de actividad:  
  
1.  Seleccione el criterio de filtrado: si desea filtrar los registros de actividad basándose en el valor de una de las columnas de la cuadrícula de actividades (basado en valores) o basándose en un intervalo de fechas, o en ambos.  
  
    1.  **Filtrado basado en valores**: seleccione un criterio de filtro en la lista **Filtrar por** y, a continuación, seleccione el valor adecuado por el que filtrar en la lista **Valor** . Al seleccionar una opción de la lista **Filtrar por** , la lista **Valor** se actualiza con los valores posibles. Puede filtrar por los campos siguientes de los registros de actividad: **Activa**, **Tipo**, **Subtipo**, **Estado actual**, **DQKB**y **Usuario**.  
  
    2.  **Filtrado basado en intervalos de fecha**: seleccione las fechas apropiadas en los controles de fecha **Desde la fecha** y **Hasta la fecha** . De forma predeterminada, la fecha mostrada en **Desde la fecha** es dos días antes de la fecha actual, y la fecha mostrada en **Hasta la fecha** es la fecha actual. El filtrado no se realiza basándose en las fechas *desde* y *hasta* propiamente dichas, sino en el intervalo. Esto significa que se mostrará cada actividad que se estaba ejecutando durante el intervalo de fechas seleccionado.  
  
2.  Haga clic en el icono **Actualizar la lista de actividades** para aplicar el filtrado y ver únicamente las actividades de DQS filtradas.  
  
##  <a name="view-dqs-activity-details"></a><a name="ActivityDetails"></a> Ver los detalles de la actividad de DQS  
 En la pantalla de supervisión de actividades puede ver información detallada acerca de una actividad de DQS, como los pasos de la actividad y la información del generador de perfiles. Para ello:  
  
1.  Seleccione una actividad de DQS en la cuadrícula de actividades (en el panel superior).  
  
2.  El panel inferior muestra los detalles de actividad de la actividad seleccionada en las 2 pestañas siguientes:  
  
    -   **Pasos de la actividad**: muestra una cuadrícula de los procesos de cálculo (pasos de la actividad) relacionados con la actividad seleccionada. En esta pestaña se pueden mostrar varios pasos de actividad para una actividad. Esto puede ocurrir si el usuario ha ejecutado varias veces el mismo paso de actividad dentro de la actividad. Por ejemplo, si el paso de actividad se ha detenido y se ha iniciado de nuevo. La cuadrícula de esta pestaña muestra la siguiente información para cada paso de actividad relacionado con la actividad: **Tipo**, **Estado actual**, **Hora de inicio**, **Tiempo transcurrido**y **Hora de finalización**.  
  
    -   **Generador de perfiles**: muestra la información sobre los perfiles para las actividades actuales y las históricas. En el caso de las actividades actuales, contiene información parcial pero coherente. La información sobre los perfiles de una actividad también se exporta a un archivo de Excel cuando se exportan al mismo los detalles de actividad correspondientes. La información está disponible en las hojas **generador de perfiles-origen** y **generador de perfiles-campos** del archivo de Excel exportado.  
  
##  <a name="export-dqs-activity-details"></a><a name="Export"></a> Exportar los detalles de la actividad de DQS  
 Puede exportar las propiedades de actividad, los procesos de actividad y la información sobre los perfiles de una actividad de la pantalla de supervisión a un archivo de Excel. Para ello:  
  
1.  Seleccione una actividad en la cuadrícula de actividades (en el panel superior).  
  
2.  Haga clic en el icono **Exportar la actividad seleccionada a Excel** . O bien, haga clic con el botón secundario en cualquier actividad de la cuadrícula de actividades y, a continuación, haga clic en **Exportar actividad** en el menú contextual.  
  
3.  Se le pedirá que especifique un nombre y una ubicación para el archivo de Excel que se va a guardar. El archivo de Excel exportado contiene las hojas siguientes:  
  
    |Nombre de la hoja|Descripción|  
    |----------------|-----------------|  
    |Actividad|Contiene información (columnas) sobre la actividad, como en la cuadrícula de actividades.|  
    |Procesos|Contiene información (columnas) sobre los procesos de la actividad, como en la pestaña **Pasos de la actividad** .|  
    |Generador de perfiles - origen|Para el subtipo **Limpieza** , contiene la información siguiente acerca de la actividad: Registros, Registros correctos, Registros corregidos y Registros no válidos.<br /><br /> Para los subtipos **Detección de conocimiento**, **Administración de dominios**, **Directiva de coincidencia**y **Coincidencia** , contiene la información siguiente acerca de la actividad: Registros, Valores totales, Nuevos valores, Valores únicos y Nuevos valores únicos.|  
    |Generador de perfiles - campos|Para los subtipos **Limpieza** y **Limpieza SSIS** , contiene la información siguiente acerca de la actividad: Campo, Dominio, Valores corregidos, Valores sugeridos, Integridad y Precisión.<br /><br /> Para los subtipos **Detección de conocimiento**, **Administración de dominios**, **Directiva de coincidencia**y **Coincidencia** , contiene la información siguiente acerca de la actividad: Campo, Dominio, Nuevo, Único, Válido en el dominio e Integridad.|  
  
##  <a name="terminate-a-dqs-activity"></a><a name="Terminate"></a> Terminar una actividad de DQS  
 Los administradores de DQS (rol dqs_administrator) pueden terminar las actividades en ejecución (activas) que no sean del tipo **Limpieza SSIS**. Si da por terminada una actividad, detendrá todos los procesos en ejecución de dicha actividad y eliminará todo lo relacionado con la misma. No se puede deshacer esta operación. Terminar una actividad en la pantalla de supervisión de actividades equivale a cancelar la actividad respectiva haciendo clic en **Cancelar** mientras se ejecuta en el área de características de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Para terminar una actividad:  
  
1.  Seleccione una actividad en ejecución en la cuadrícula de actividades (en el panel superior).  
  
2.  Haga clic en el icono **Terminar la actividad seleccionada** . O bien, haga clic con el botón secundario en la actividad en la cuadrícula de actividades y, a continuación, haga clic en **Terminar actividad** en el menú contextual.  
  
3.  Se muestra un mensaje para confirmar la acción. Haga clic en **Sí**.  
  
##  <a name="stop-a-process-in-dqs-activity"></a><a name="Stop"></a> Detener un proceso en una actividad de DQS  
 Los administradores de DQS (rol dqs_administrator) pueden detener un proceso en ejecución (activo) en las actividades que no sean del tipo **Limpieza SSIS**. Detener un proceso en la pantalla de supervisión de actividades equivale a detener el proceso dentro de la actividad respectiva en el área de características de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Por ejemplo, detener el proceso de limpieza asistido por PC dentro de una actividad de limpieza, o detener el proceso de búsqueda de coincidencias dentro de una actividad de búsqueda de coincidencias. Un proceso detenido no se puede reiniciar desde la pantalla de supervisión de actividades. Tendrá que reiniciarlo desde el área de características respectiva del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. En ese caso, se agrega una fila adicional a la cuadrícula de procesos de la pestaña pasos de la **actividad** . El estado del proceso detenido sigue mostrándose **detenido**. Para detener un proceso:  
  
1.  Seleccione un proceso en ejecución en la cuadrícula de detalles de la actividad (en el panel inferior).  
  
2.  Haga clic en el icono **Detener el proceso seleccionado** . O bien, haga clic con el botón secundario en la cuadrícula de detalles de la actividad y, a continuación, haga clic en **Detener proceso** en el menú contextual.  
  
3.  Se muestra un mensaje para confirmar la acción. Haga clic en **Sí**.  
  
  
