---
title: Conjunto de filas DISCOVER_XML_METADATA | Microsoft Docs
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
api_name:
- DISCOVER_XML_METADATA
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_XML_METADATA rowset
ms.assetid: 0befd026-db1b-43ac-b0e6-734abb56a4b1
caps.latest.revision: 40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 616e7c06087fff3d2c2e0388ba44a3e30b200e5f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37214015"
---
# <a name="discoverxmlmetadata-rowset"></a>Conjunto de filas DISCOVER_XML_METADATA
  Devuelve un documento XML que describe un objeto solicitado. El conjunto de filas que se devuelve siempre consta de una fila y una columna.  
  
 Si se llama a la [Discover](../../xmla/xml-elements-methods-discover.md) método con el `DISCOVER_XML_METATDATA` valor de enumeración en el [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, el `Discover` método devuelve el `DISCOVER_XML_METATDATA` conjunto de filas.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas `DISCOVER_XML_METADATA` contiene la columna siguiente.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`METADATA`|`DBTYPE_WSTR`||Documento XML que describe el objeto solicitado por la restricción.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
> [!IMPORTANT]  
>  El conjunto de filas `DISCOVER_XML_METADATA` no se puede consultar mediante la sintaxis del comando SELECT. Sin embargo, el conjunto de filas `DISCOVER_XML_METADATA` se puede consultar usando <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_XML_METADATA` conjunto de filas puede tener restricciones en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`DatabaseID`|`DBTYPE_WSTR`|Opcional.|  
|`DimensionID`|`DBTYPE_WSTR`|Opcional.|  
|`CubeID`|`DBTYPE_WSTR`|Opcional.|  
|`MeasureGroupID`|`DBTYPE_WSTR`|Opcional.|  
|`PartitionID`|`DBTYPE_WSTR`|Opcional.|  
|`PerspectiveID`|`DBTYPE_WSTR`|Opcional.|  
|`DimensionPermissionID`|`DBTYPE_WSTR`|Opcional.|  
|`RoleID`|`DBTYPE_WSTR`|Opcional.|  
|`DatabasePermissionID`|`DBTYPE_WSTR`|Opcional.|  
|`MiningModelID`|`DBTYPE_WSTR`|Opcional.|  
|`MiningModelPermissionID`|`DBTYPE_WSTR`|Opcional.|  
|`DataSourceID`|`DBTYPE_WSTR`|Opcional.|  
|`MiningStructureID`|`DBTYPE_WSTR`|Opcional.|  
|`AggregationDesignID`|`DBTYPE_WSTR`|Opcional.|  
|`TraceID`|`DBTYPE_WSTR`|Opcional.|  
|`MiningStructurePermissionID`|`DBTYPE_WSTR`|Opcional.|  
|`CubePermissionID`|`DBTYPE_WSTR`|Opcional.|  
|`AssemblyID`|`DBTYPE_WSTR`|Opcional.|  
|`MdxScriptID`|`DBTYPE_WSTR`|Opcional.|  
|`DataSourceViewID`|`DBTYPE_WSTR`|Opcional.|  
|`DataSourcePermissionID`|`DBTYPE_WSTR`|Opcional.|  
|`ObjectExpansion`|`DBTYPE_WSTR`|Opcional.|  
  
 La restricción, `ObjectExpansion`, está disponible para todos los objetos principales de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. El cliente normalmente usa las restricciones para describir los objetos OLAP para los que se va a devolver el DDL y utiliza la restricción `ObjectExpansion` para definir el grado de expansión en el DDL devuelto. En la tabla siguiente indica si se permite el valor de enumeración para [elemento Alter &#40;XMLA&#41; ](../../xmla/xml-elements-commands/alter-element-xmla.md) comandos.  
  
|Valor de enumeración|Descripción|  
|-----------------------|-----------------|  
|`ReferenceOnly`|Devuelve solamente el nombre, identificador, marca de tiempo y estado requeridos para los objetos solicitados y todos los objetos principales descendientes de forma recursiva.|  
|`ObjectProperties`|Expande el objeto solicitado sin referencias a los objetos contenidos (incluye los objetos secundarios contenidos expandidos).|  
|`ExpandObject`|Igual que *ObjectProperties*, pero también devuelve el nombre, identificador y marca de tiempo de los objetos principales contenidos.|  
|`ExpandFull`|Expande totalmente el objeto solicitado de forma recursiva hasta el final de cada objeto contenido.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  
