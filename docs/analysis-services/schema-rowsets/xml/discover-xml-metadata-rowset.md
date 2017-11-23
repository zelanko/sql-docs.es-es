---
title: Conjunto de filas DISCOVER_XML_METADATA | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DISCOVER_XML_METADATA
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_XML_METADATA rowset
ms.assetid: 0befd026-db1b-43ac-b0e6-734abb56a4b1
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8b53ac5b9c24da68c50fa06644e80389ac53f509
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="discoverxmlmetadata-rowset"></a>Conjunto de filas DISCOVER_XML_METADATA
  Devuelve un documento XML que describe un objeto solicitado. El conjunto de filas que se devuelve siempre consta de una fila y una columna.  
  
 Si se llama a la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método con el **DISCOVER_XML_METATDATA** valor de enumeración en el [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, el **Discover**método devuelve el **DISCOVER_XML_METATDATA** conjunto de filas.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El conjunto de filas **DISCOVER_XML_METADATA** contiene la columna siguiente.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**METADATOS**|**DBTYPE_WSTR**||Documento XML que describe el objeto solicitado por la restricción.|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
> [!IMPORTANT]  
>  El conjunto de filas **DISCOVER_XML_METADATA** no se puede consultar mediante la sintaxis del comando SELECT. Sin embargo, el **DISCOVER_XML_METADATA** conjunto de filas se pueden consultar mediante <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_XML_METADATA** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**DatabaseID**|**DBTYPE_WSTR**|Opcional.|  
|**DimensionID**|**DBTYPE_WSTR**|Opcional.|  
|**CubeID**|**DBTYPE_WSTR**|Opcional.|  
|**MeasureGroupID**|**DBTYPE_WSTR**|Opcional.|  
|**PartitionID**|**DBTYPE_WSTR**|Opcional.|  
|**PerspectiveID**|**DBTYPE_WSTR**|Opcional.|  
|**DimensionPermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**RoleID**|**DBTYPE_WSTR**|Opcional.|  
|**DatabasePermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**MiningModelID**|**DBTYPE_WSTR**|Opcional.|  
|**MiningModelPermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**DataSourceID**|**DBTYPE_WSTR**|Opcional.|  
|**MiningStructureID**|**DBTYPE_WSTR**|Opcional.|  
|**AggregationDesignID**|**DBTYPE_WSTR**|Opcional.|  
|**TraceID**|**DBTYPE_WSTR**|Opcional.|  
|**MiningStructurePermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**CubePermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**AssemblyID**|**DBTYPE_WSTR**|Opcional.|  
|**MdxScriptID**|**DBTYPE_WSTR**|Opcional.|  
|**DataSourceViewID**|**DBTYPE_WSTR**|Opcional.|  
|**DataSourcePermissionID**|**DBTYPE_WSTR**|Opcional.|  
|**ObjectExpansion**|**DBTYPE_WSTR**|Opcional.|  
  
 La restricción, **ObjectExpansion**, está disponible para todos los objetos principales de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. El cliente normalmente usa las restricciones para describir los objetos OLAP para los que se va a devolver el DDL y utiliza la restricción **ObjectExpansion** para definir el grado de expansión en el DDL devuelto. En la tabla siguiente indica si se permite el valor de enumeración para [Modificar elemento &#40; XMLA &#41; ](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comandos.  
  
|Valor de enumeración|Description|  
|-----------------------|-----------------|  
|**ReferenceOnly**|Devuelve solamente el nombre, identificador, marca de tiempo y estado requeridos para los objetos solicitados y todos los objetos principales descendientes de forma recursiva.|  
|**ObjectProperties**|Expande el objeto solicitado sin referencias a los objetos contenidos (incluye los objetos secundarios contenidos expandidos).|  
|**ExpandObject**|Igual que *ObjectProperties*, pero también devuelve el nombre, identificador y marca de tiempo de los objetos principales contenidos.|  
|**ExpandFull**|Expande totalmente el objeto solicitado de forma recursiva hasta el final de cada objeto contenido.|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
