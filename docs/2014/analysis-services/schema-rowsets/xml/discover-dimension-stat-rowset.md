---
title: Conjunto de filas DISCOVER_DIMENSION_STAT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 639f8cd7-3b43-40d5-8b84-552daf60d484
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d70382117367762dc35a6d02663f54436ea63bb3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37289742"
---
# <a name="discoverdimensionstat-rowset"></a>Conjunto de filas DISCOVER_DIMENSION_STAT
  Proporciona información acerca de una dimensión, incluida la base de datos que lo contiene, el nombre de la dimensión, sus atributos y un recuento de los miembros para cada atributo. En un modelo tabular, corresponde a las columnas de una tabla y el número de valores de cada columna.  
  
 **Se aplica a:** modelos tabulares, modelos multidimensionales  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_DIMENSION_STAT` conjunto de filas contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Obligatorio|Nombre de la base de datos que contiene la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`|Obligatorio|Nombre de la dimensión.<br /><br /> Esta columna se requiere en la lista de restricciones.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||Nombre de un atributo en la dimensión.|  
|`ATTRIBUTE_COUNT`|`DBTYPE_I8`||Recuento de valores del atributo con nombre. Para un modelo tabular, el valor es siempre igual al número de filas de la tabla.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd90-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
