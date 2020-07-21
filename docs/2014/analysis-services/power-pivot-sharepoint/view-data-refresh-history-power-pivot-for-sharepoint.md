---
title: Ver el historial de actualización de datos (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- data refresh history [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 4c8d8aa8-794d-4f72-ace3-78d0e688e1a5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6ad05ca790b42756a51f0dfc419d369e8a24f70d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547687"
---
# <a name="view-data-refresh-history-powerpivot-for-sharepoint"></a>Ver el Historial de actualización de datos (PowerPivot para SharePoint)
  El historial de actualización de datos es un registro de toda la actividad de actualización de datos para los datos PowerPivot en un libro de Excel. Las operaciones de actualización de datos se realizan en una instancia del servidor de Analysis Services en una granja de servidores de SharePoint según la programación que se proporcione. De forma predeterminada, el historial de la actualización de datos se retiene durante un año. Sin embargo, el administrador de una granja de servidores puede especificar una directiva de retención diferente para el historial de uso y eventos que determine durante cuánto tiempo se mantienen los registros de actualización de datos.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2013 | SharePoint 2010  
  
 **En este tema:**  
  
 [Requisitos previos](#prereq)  
  
 [Ver el historial de actualización de datos para un libro individual](#viewhistory)  
  
 [Ver el historial de actualización de datos para todos los libros](#viewITOps)  
  
 [Usar la información del historial](#pageelements)  
  
##  <a name="prerequisites"></a><a name="prereq"></a> Requisitos previos  
 Debe tener los permisos de contribución u otros superiores para ver el historial de la actualización de datos.  
  
 Debe haber habilitado y programado la actualización de datos en un libro que contenga los datos PowerPivot. Si no ha programado la actualización de datos, verá la página de definición de la programación en lugar de la información del historial.  
  
##  <a name="view-data-refresh-history-for-an-individual-workbook"></a><a name="viewhistory"></a>Ver el historial de actualización de datos para un libro individual  
  
1.  En un sitio de SharePoint, abra la biblioteca que contiene un libro de Excel con los datos PowerPivot.  
  
     No hay ningún indicador visual que identifique qué libros en una biblioteca de SharePoint contienen datos PowerPivot. Debe saber de antemano qué libro contiene los datos PowerPivot actualizables.  
  
2.  Seleccione el libro y, a continuación, haga clic en la flecha abajo que aparece a la derecha.  
  
3.  Seleccione **Administrar actualización de datos PowerPivot**.  
  
 La página del historial aparece y muestra un registro completo de toda la actividad de actualización para los datos PowerPivot del libro de Excel actual.  
  
##  <a name="view-data-refresh-history-for-all-workbooks"></a><a name="viewITOps"></a>Ver el historial de actualización de datos para todos los libros  
 Mediante el panel de administración de PowerPivot de Administración central, los administradores de una granja y los administradores de las aplicaciones de servicio pueden obtener una vista completa del historial de la actualización de datos y del estado de todos los libros PowerPivot. Para obtener más información, vea [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="use-history-information"></a><a name="pageelements"></a>Usar información del historial  
 La página del historial de actualización de datos proporciona información detallada sobre cada operación de actualización. Puede utilizar la información de esta página para confirmar si la actualización tuvo lugar o determinar por qué se produjo un error.  
  
|Elemento|Descripción|  
|----------|-----------------|  
|Nombre|Especifica el nombre de archivo del libro de Excel que contiene los datos PowerPivot.|  
|Estado actual|Los valores son **Programado**, **Actualizando**, **Correcto**o **Error**.<br /><br /> **Programado** aparece cuando se crea por primera vez la programación. Después de que la actualización de datos se ejecuta la primera vez, este mensaje de estado ya no aparece.<br /><br /> **Actualizando** indica que la actualización de datos está en curso. Una solicitud está en la cola de procesos o ejecutándose activamente en el servidor.<br /><br /> **Correcto** indica que la última operación de actualización de datos se completó y que el libro actualizado se vuelve a poner en la biblioteca de SharePoint.<br /><br /> **Error** indica que la última operación de actualización de datos no tuvo éxito. Los datos actualizados no se guardaron. El libro contiene los mismos datos que tenía antes de que la actualización de datos comenzara.|  
|Última actualización correcta|Especifica la fecha en la que la última actualización de datos se completó correctamente.|  
|Siguiente actualización de programación|Especifica la fecha en la que la siguiente actualización de datos está programada para que se produzca.<br /><br /> El vínculo **Configurar programación** le lleva a la página de definición de la programación. Si tiene permisos de contribución en el libro, puede hacer clic en el vínculo para ver y modificar la información de programación que controla la actualización de datos desatendida de los datos PowerPivot del libro.|  
|Comenzado|Dentro de la sección de detalles del historial, **Iniciado** indica el tiempo de proceso real. El tiempo de procesamiento real podría ser diferente de lo que programó. El procesamiento comenzará cuando haya memoria suficiente disponible en el servidor. Si el servidor está muy ocupado, el procesamiento podría comenzar varias horas después de la hora de inicio que especificó.|  
|Completado|Dentro de la sección de detalles del historial, **Completado** indica cuándo finalizó la operación de la actualización de datos. La fecha y hora indica cuándo se volvió a incluir el libro en la biblioteca.<br /><br /> Si se produce un error en la actualización de los datos, uno o más mensajes de error explican su causa. Puede expandir cada registro para ver el estado detallado. Cada origen de datos se enumera individualmente, junto con los mensajes de éxito o de error que explican por qué la actualización de datos no se completó.|  
|Time|Proporciona el tiempo acumulado desde el momento en que se inició la actualización de datos hasta que se completó.|  
|Estado|Proporciona un registro histórico de si una operación de actualización se realizó correctamente o no.|  
  
## <a name="see-also"></a>Consulte también  
 [Configurar la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Actualización de datos PowerPivot](power-pivot-data-refresh.md)  
  
  
