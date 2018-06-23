---
title: Informes para el servidor de Integration Services | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.SWB.SUMMARY.RENDER.CUSTOM.REPORT.F1
ms.assetid: e976e7c0-a805-4370-bf73-356c8e3becfb
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9809de19a363c94365c0da88655d4e54b81b80cd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203226"
---
# <a name="reports-for-the-integration-services-server"></a>Informes para el servidor de Integration Services
  En la versión actual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], existen informes estándares en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para ayudarle a supervisar [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proyectos que se han implementado en el [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] server. Estos informes le ayudan a ver el estado y historial de los paquetes y, si es necesario, identificar la causa de los errores de ejecución de paquetes.  
  
 En la parte superior de cada página de informe, el icono Atrás le lleva a la página que vio anteriormente, el icono Actualizar actualiza la información que se muestra en la página y el icono Imprimir le permite imprimir la página actual.  
  
 Para más información sobre cómo implementar paquetes en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , vea [Implementar proyectos en el servidor de Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
## <a name="integration-services-dashboard"></a>Panel de Integration Services  
 El informe **Panel de Integration Services** proporciona información general sobre todas las ejecuciones de paquetes de la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para cada paquete que se ha ejecutado en el servidor, el panel le permite 'acercar' para buscar detalles específicos sobre los errores que podrían haberse producido durante la ejecución del paquete.  
  
 El informe muestra las siguientes secciones de información.  
  
|Sección|Descripción|  
|-------------|-----------------|  
|**Información de ejecución**|Muestra el número de ejecuciones en distintos estados (error, en ejecución, correcto, otros) en las últimas 24 horas.|  
|**Información del paquete**|Muestra el número total de paquetes que se han ejecutado en las últimas 24 horas.|  
|**Información de conexión**|Muestra las conexiones que se han usado en las ejecuciones con error en las últimas 24 horas.|  
|**Información detallada del paquete**|Muestra los detalles de las ejecuciones completadas que se han realizado en las últimas 24 horas. Por ejemplo, esta sección muestra el número de ejecuciones con errores frente al número total de ejecuciones, la duración de las ejecuciones (en segundos) y la duración promedio de las ejecuciones durante los últimos tres meses.<br /><br /> Puede ver información adicional sobre un paquete si hace clic en **Información general**, **Todos los mensajes**y **Rendimiento de la ejecución**.<br /><br /> El informe **Rendimiento de la ejecución** muestra la duración de la última instancia de ejecución, así como las horas de inicio y de finalización, y el entorno que se aplicó.<br /><br /> El gráfico y la tabla asociada incluidos en el informe **Rendimiento de la ejecución** muestran la duración de las 10 últimas ejecuciones correctas del paquete. La tabla muestra también la duración promedio de ejecución durante un período de tres meses. Pueden haberse aplicado diferentes entornos y valores literales en tiempo de ejecución para estas 10 ejecuciones correctas del paquete.<br /><br /> Por último, el informe **Rendimiento de la ejecución** muestra el Tiempo activo y el TIempo total para los componentes de flujo de datos del paquete. El Tiempo activo se refiere al tiempo total que el componente ha pasado ejecutándose en todas las fases y el Tiempo total se refiere al tiempo total transcurrido para un componente. El informe solo muestra esta información para los componentes del paquete cuando el nivel de registro de la ejecución del último paquete se estableció en Performance (Rendimiento) o Verbose (Detallado).<br /><br /> El informe **Información general** muestra el estado de las tareas del paquete. El informe **Mensajes** muestra los mensajes de eventos y los mensajes de error para el paquete y las tareas, como las horas de inicio y de finalización, y el número de filas escritas.<br /><br /> También puede hacer clic **Ver mensajes** en el informe **Información general** para navegar al informe **Mensajes** . También puede hacer clic **Ver información general** en el informe **Mensajes** para navegar al informe **Información general** .|  
  
 Puede filtrar la tabla que se muestra en cualquier página si hace clic en **Filtro** y selecciona los criterios deseados en el cuadro de diálogo **Configuración de filtro** . Los criterios de filtro disponibles dependen de los datos que se muestran. Puede cambiar el criterio de ordenación del informe haciendo clic en el icono de ordenación del cuadro de diálogo **Configuración de filtro** .  
  
## <a name="all-executions-report"></a>Informe Todas las ejecuciones  
 El informe **Todas las ejecuciones** muestra un resumen de todas las ejecuciones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] realizadas en el servidor. Puede haber varias ejecuciones del paquete de ejemplo. A diferencia del informe **Panel de Integration Services** , puede configurar el informe **Todas las ejecuciones** para que muestre las ejecuciones que se han iniciado durante un intervalo de fechas. Las fechas pueden abarcar varios días, meses o años.  
  
 El informe muestra las siguientes secciones de información.  
  
|Sección|Descripción|  
|-------------|-----------------|  
|Filtro|Muestra el filtro actual que se aplica al informe, como el Intervalo de tiempo de inicio.|  
|Información de ejecución|Muestra la hora de inicio, la hora de finalización y la duración de cada ejecución del paquete. Puede ver una lista de los valores de parámetro usados con una ejecución de paquete, como los valores que se pasaron a un paquete secundario mediante la tarea Ejecutar paquete. Para ver la lista de parámetros, haga clic en Información general.|  
  
 Para obtener más información sobre cómo utilizar la tarea Ejecutar paquete con el fin de que los valores estén disponibles para un paquete secundario, vea [Execute Package Task](control-flow/execute-package-task.md).  
  
 Para más información sobre los parámetros, vea [Parámetros de Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="all-connections"></a>Todas las conexiones  
 El informe **Todas las conexiones** proporciona la siguiente información para las conexiones con errores, para las ejecuciones que se ha realizado en la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 El informe muestra las siguientes secciones de información.  
  
|Sección|Descripción|  
|-------------|-----------------|  
|Filter|Muestra el filtro actual que se aplica al informe, como conexiones con una cadena especificada y el intervalo de **Hora del último error** .<br /><br /> Establezca el intervalo de **Hora del último error** para que se muestren solo los errores de conexión que se produjeron durante un intervalo de fechas. El intervalo puede abarcar varios días, meses o años.|  
|Detalles|Muestra la cadena de conexión, el número de ejecuciones en las que se produjo un error de conexión y la fecha en la que hubo un error de conexión por última vez.|  
  
## <a name="all-operations-report"></a>Informe Todas las operaciones  
 El informe **Todas las operaciones** muestra un resumen de todas las operaciones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] realizadas en el servidor, incluidas las de implementación, validación y ejecución de paquetes, así como otras operaciones administrativas. Al igual que con el Panel de Integration Services, puede aplicar un filtro a la tabla para reducir la información mostrada.  
  
## <a name="all-validations-report"></a>Informe Todas las validaciones  
 El informe **Todas las validaciones** muestra un resumen de todas las validaciones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] realizadas en el servidor. El resumen muestra información para cada validación, como el estado, la hora de inicio y la hora de finalización. Cada entrada de resumen incluye un vínculo a los mensajes generados durante la validación. Al igual que con el Panel de Integration Services, puede aplicar un filtro a la tabla para reducir la información mostrada.  
  
## <a name="custom-reports"></a>informes personalizados  
 Puede agregar un informe personalizado (archivo .rdl) al nodo del catálogo de **SSISDB** en el nodo **Catálogos de Integration Services** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Antes de agregar el informe, confirme que usa una convención de nomenclatura de tres partes para calificar completamente los objetos a los que hace referencia como una tabla de origen. De lo contrario, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] mostrará un error. La convención de nomenclatura es \<base de datos>.\<propietario>.\<objeto>. Un ejemplo sería SSISDB.internal.executions.  
  
> [!NOTE]  
>  Al agregar informes personalizados al nodo **SSISDB** en el nodo **Bases de datos** , el prefijo de SSISDB no es necesario.  
  
 Para obtener instrucciones sobre cómo agregar y agregar un informe personalizado, vea [Add a Custom Report to Management Studio](../ssms/object/add-a-custom-report-to-management-studio.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Ver los informes para el servidor de Integration Services](../../2014/integration-services/view-reports-for-the-integration-services-server.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Supervisión de ejecuciones de paquetes y otras operaciones](performance/monitor-running-packages-and-other-operations.md)  
  
  