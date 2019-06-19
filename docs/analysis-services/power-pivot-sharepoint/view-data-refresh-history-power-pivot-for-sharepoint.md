---
title: Ver historial (PowerPivot para SharePoint) de la actualización de datos | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 355ade7f4c90b595356efc5d39c2fa7cf587b11b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62509954"
---
# <a name="view-data-refresh-history-power-pivot-for-sharepoint"></a>Ver el Historial de actualización de datos (Power Pivot para SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El historial de actualización de datos es un registro de toda la actividad de actualización de datos para los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un libro de Excel. Las operaciones de actualización de datos se realizan en una instancia del servidor de Analysis Services en una granja de servidores de SharePoint según la programación que se proporcione. De forma predeterminada, el historial de la actualización de datos se retiene durante un año. Sin embargo, el administrador de una granja de servidores puede especificar una directiva de retención diferente para el historial de uso y eventos que determine durante cuánto tiempo se mantienen los registros de actualización de datos.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **En este tema:**  
  
 [Requisitos previos](#prereq)  
  
 [Ver el historial de actualización de datos para un libro individual](#viewhistory)  
  
 [Ver el historial de actualización de datos para todos los libros](#viewITOps)  
  
 [Usar la información del historial](#pageelements)  
  
##  <a name="prereq"></a> Requisitos previos  
 Debe tener los permisos de contribución u otros superiores para ver el historial de la actualización de datos.  
  
 Debe haber habilitado y programado la actualización de datos en un libro que contenga los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Si no ha programado la actualización de datos, verá la página de definición de la programación en lugar de la información del historial.  
  
##  <a name="viewhistory"></a> Ver el historial de actualización de datos para un libro individual  
  
1.  En un sitio de SharePoint, abra la biblioteca que contiene un libro de Excel con los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
     No hay ningún indicador visual que identifique qué libros en una biblioteca de SharePoint contienen datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Debe saber de antemano qué libro contiene los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] actualizables.  
  
2.  Seleccione el libro y, a continuación, haga clic en la flecha abajo que aparece a la derecha.  
  
3.  Seleccione **Administrar actualización de datos de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]** .  
  
 La página del historial aparece y muestra un registro completo de toda la actividad de actualización para los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] del libro de Excel actual.  
  
##  <a name="viewITOps"></a> Ver el historial de actualización de datos para todos los libros  
 Mediante el panel de administración de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] de Administración central, los administradores de una granja y los administradores de las aplicaciones de servicio pueden obtener una vista completa del historial de la actualización de datos y del estado de todos los libros [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para más información, consulte [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="pageelements"></a> Usar la información del historial  
 La página del historial de actualización de datos proporciona información detallada sobre cada operación de actualización. Puede utilizar la información de esta página para confirmar si la actualización tuvo lugar o determinar por qué se produjo un error.  
  
|Elemento|Descripción|  
|----------|-----------------|  
|NOMBRE|Especifica el nombre de archivo del libro de Excel que contiene los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Estado actual|Los valores son **Programado**, **Actualizando**, **Correcto**o **Error**.<br /><br /> **Programado** aparece cuando se crea por primera vez la programación. Después de que la actualización de datos se ejecuta la primera vez, este mensaje de estado ya no aparece.<br /><br /> **Actualizando** indica que la actualización de datos está en curso. Una solicitud está en la cola de procesos o ejecutándose activamente en el servidor.<br /><br /> **Correcto** indica que la última operación de actualización de datos se completó y que el libro actualizado se vuelve a poner en la biblioteca de SharePoint.<br /><br /> **Error** indica que la última operación de actualización de datos no tuvo éxito. Los datos actualizados no se guardaron. El libro contiene los mismos datos que tenía antes de que la actualización de datos comenzara.|  
|Última actualización correcta|Especifica la fecha en la que la última actualización de datos se completó correctamente.|  
|Siguiente actualización de programación|Especifica la fecha en la que la siguiente actualización de datos está programada para que se produzca.<br /><br /> El vínculo **Configurar programación** le lleva a la página de definición de la programación. Si tiene permisos de contribución en el libro, puede hacer clic en el vínculo para ver y modificar la información de programación que controla la actualización de datos desatendida de los datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] del libro.|  
|Iniciado|Dentro de la sección de detalles del historial, **Iniciado** indica el tiempo de proceso real. El tiempo de procesamiento real podría ser diferente de lo que programó. El procesamiento comenzará cuando haya memoria suficiente disponible en el servidor. Si el servidor está muy ocupado, el procesamiento podría comenzar varias horas después de la hora de inicio que especificó.|  
|Completada|Dentro de la sección de detalles del historial, **Completado** indica cuándo finalizó la operación de la actualización de datos. La fecha y hora indica cuándo se volvió a incluir el libro en la biblioteca.<br /><br /> Si se produce un error en la actualización de los datos, uno o más mensajes de error explican su causa. Puede expandir cada registro para ver el estado detallado. Cada origen de datos se enumera individualmente, junto con los mensajes de éxito o de error que explican por qué la actualización de datos no se completó.|  
|Time|Proporciona el tiempo acumulado desde el momento en que se inició la actualización de datos hasta que se completó.|  
|Estado|Proporciona un registro histórico de si una operación de actualización se realizó correctamente o no.|  
  
## <a name="see-also"></a>Vea también  
 [Configurar la recolección de datos de uso para Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Programar una actualización de datos (Power Pivot para SharePoint)](http://msdn.microsoft.com/8571208f-6aae-4058-83c6-9f916f5e2f9b)   
 [Actualización de datos PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  
