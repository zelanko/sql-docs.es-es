---
title: Cuadro de diálogo Filtrar (Complemento MDS para Excel) | Microsoft Docs
ms.custom: microsoft-excel-add-in
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: b987b141-5abf-4161-a073-4cfc3e7f5aae
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 0ae5e6ad40a9a4c071ca452d893ca6644dae133d
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52403900"
---
# <a name="filter-dialog-box-mds-add-in-for-excel"></a>Cuadro de diálogo Filtrar (Complemento MDS para Excel)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], use el cuadro de diálogo **Filtro** para restringir la lista de datos administrados por MDS antes de cargarla en Excel.  
  
 Este cuadro de diálogo contiene tres secciones: **Columnas**, **Filas**, y **Resumen**.  
  
## <a name="columns"></a>Columnas  
 Use la sección **Columnas** para determinar los atributos (columnas) que quiere mostrar en Excel.  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|Tipo de atributo|Un tipo de atributo describe el tipo de miembros con los que desea trabajar. En la mayoría de los casos, es **Hoja**. Para obtener más información sobre los tipos de miembros, consulte [Miembros &#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md).|  
|Jerarquía explícita|Si elige el tipo de atributo **Consolidado** , elija la jerarquía a la que pertenecen los miembros consolidados. Para obtener más información, consulte [Jerarquías explícitas &#40;Master Data Services&#41;](../../master-data-services/explicit-hierarchies-master-data-services.md).|  
|Grupos de atributos|Los grupos de atributos son una manera de agrupar subconjuntos de atributos. Elija un grupo de atributos si desea mostrar un subconjunto de atributos disponibles. Para obtener más información sobre los grupos de atributos, consulte [Grupos de atributos &#40;Master Data Services&#41;](../../master-data-services/attribute-groups-master-data-services.md).|  
|Seleccionar todo|Haga clic para seleccionar todos los atributos mostrados en la lista.|  
|Borrar todo|Haga clic para borrar los atributos seleccionados mostrados en la lista.<br /><br /> No puede borrar **Nombre** ni **Código**.|  
|Flecha arriba/flecha abajo|Haga clic para subir y bajar el atributo seleccionado en la lista. El orden de arriba a abajo corresponde al orden de izquierda a derecha en el que se muestran las columnas en la hoja.|  
  
## <a name="rows"></a>Filas  
 Use la sección **Filas** para determinar los miembros (filas) que quiere mostrar en Excel. Para ello, defina criterios para filtrar las filas que se muestran.  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|Attribute|Muestra un atributo por el que desea filtrar. Si no aparece ningún atributo, se debe a que no se han agregado.<br /><br /> Nota: Puede filtrar los atributos que no tiene previsto mostrar en la hoja de cálculo.|  
|Operador|Muestra los operadores correspondientes al tipo de atributo que estaba seleccionado. Para obtener más información, consulte [Operadores de filtro &#40;Master Data Services&#41;](../../master-data-services/filter-operators-master-data-services.md).|  
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
  
## <a name="see-also"></a>Ver también  
 [Filtrar los datos antes de exportar &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/filter-data-before-exporting-mds-add-in-for-excel.md)   
 [Información general: Exportar datos a Excel &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
  
