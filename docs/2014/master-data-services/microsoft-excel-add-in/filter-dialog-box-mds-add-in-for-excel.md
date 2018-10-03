---
title: Cuadro de diálogo Filtrar (Complemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
ms.assetid: b987b141-5abf-4161-a073-4cfc3e7f5aae
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: fabc7fef47a3d80427e9a4c0ef4587f4dc13f405
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140555"
---
# <a name="filter-dialog-box-mds-add-in-for-excel"></a>Cuadro de diálogo Filtrar (Complemento MDS para Excel)
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], use el cuadro de diálogo **Filtro** para restringir la lista de datos administrados por MDS antes de cargarla en Excel.  
  
 Este cuadro de diálogo contiene tres secciones: **Columnas**, **Filas**, y **Resumen**.  
  
## <a name="columns"></a>Columnas  
 Use la sección **Columnas** para determinar los atributos (columnas) que quiere mostrar en Excel.  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|Tipo de atributo|Un tipo de atributo describe el tipo de miembros con los que desea trabajar. En la mayoría de los casos, es **Hoja**. Para obtener más información sobre los tipos de miembros, consulte [Miembros &#40;Master Data Services&#41;](../members-master-data-services.md).|  
|Jerarquía explícita|Si elige el tipo de atributo **Consolidado** , elija la jerarquía a la que pertenecen los miembros consolidados. Para obtener más información, consulte [Jerarquías explícitas &#40;Master Data Services&#41;](../explicit-hierarchies-master-data-services.md).|  
|Grupos de atributos|Los grupos de atributos son una manera de agrupar subconjuntos de atributos. Elija un grupo de atributos si desea mostrar un subconjunto de atributos disponibles. Para obtener más información sobre los grupos de atributos, consulte [Grupos de atributos &#40;Master Data Services&#41;](../attribute-groups-master-data-services.md).|  
|Seleccionar todo|Haga clic para seleccionar todos los atributos mostrados en la lista.|  
|Borrar todo|Haga clic para borrar los atributos seleccionados mostrados en la lista.<br /><br /> Nota: No se puede borrar **nombre** y **código**.|  
|Flecha arriba|Haga clic para mover el atributo seleccionado hacia arriba en la lista. El orden de arriba a abajo corresponde al orden de izquierda a derecha en el que se muestran las columnas en la hoja.|  
|Flecha abajo|Haga clic para mover el atributo seleccionado hacia abajo en la lista. El orden de arriba a abajo corresponde al orden de izquierda a derecha en el que se muestran las columnas en la hoja.|  
  
## <a name="rows"></a>Filas  
 Use la sección **Filas** para determinar los miembros (filas) que quiere mostrar en Excel. Para ello, defina criterios para filtrar las filas que se muestran.  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|Attribute|Muestra un atributo por el que desea filtrar. Si no aparece ningún atributo, se debe a que no se han agregado.<br /><br /> Nota: Puede filtrar los atributos que no tiene previsto mostrar en la hoja de cálculo.|  
|Operador|Muestra los operadores correspondientes al tipo de atributo que estaba seleccionado. Para obtener más información, consulte [Operadores de filtro &#40;Master Data Services&#41;](../filter-operators-master-data-services.md).|  
|Criterios|Los criterios por los que desea filtrar.|  
|Resumen de actualización|Cuando trabaje con conjuntos de datos grandes, haga clic para actualizar la sección **Resumen** con detalles de la cantidad de datos que se cargarán.|  
|Agregar|Al hacer clic en un atributo en la sección **Columnas** y, a continuación, hacer clic en **Agregar**, se agrega un atributo a la lista de filtros.|  
|Quitar todo|Quita todos los filtros de la lista.|  
|Quitar|Quita el filtro seleccionado de la lista.|  
  
## <a name="summary"></a>Resumen  
 Use la sección **Resumen** para ver los detalles de la cantidad de datos que se cargarán, antes de cargarlos.  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|Modelo|Nombre del modelo.|  
|Versión|El nombre de la versión.|  
|Entidad|Nombre de la entidad.|  
|Filas|El número de filas que se cargan en Excel, basado en los filtros aplicados en la sección **Filas** .|  
|Columnas|El número de columnas que se cargarán en Excel, en función de los atributos seleccionados en la sección **Columnas** .|  
  
## <a name="see-also"></a>Vea también  
 [Filtrar datos antes de cargarlos &#40;complemento MDS para Excel&#41;](filter-data-before-exporting-mds-add-in-for-excel.md)   
 [Cargando datos &#40;complemento MDS para Excel&#41;](overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
