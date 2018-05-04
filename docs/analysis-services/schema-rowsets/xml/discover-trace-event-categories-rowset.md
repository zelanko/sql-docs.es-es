---
title: Conjunto de filas DISCOVER_TRACE_EVENT_CATEGORIES | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 1ad74fd2-4740-469d-85b5-abf0171737fd
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0fe97a387056fff384d34b65c96ba5cfed5d7aca
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="discovertraceeventcategories-rowset"></a>Conjunto de filas DISCOVER_TRACE_EVENT_CATEGORIES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Muestra la lista de categorías de eventos que admite el proveedor de seguimiento.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_TRACE_EVENT_CATEGORIES** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**Datos**|**DBTYPE_WSTR**||Contiene una cadena XML codificada que describe la información de categoría de eventos en el proveedor de seguimiento, incluido el nombre de categoría, el tipo y la descripción. El tipo es una cadena que indica el tipo de categoría. Los valores de enumeración son los siguientes:<br /><br /> 0=normal<br /><br /> 1=significativo<br /><br /> 2=Error|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd19-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACE_EVENT_CATEGORIES|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
