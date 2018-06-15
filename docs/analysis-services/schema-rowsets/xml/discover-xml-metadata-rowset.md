---
title: Conjunto de filas DISCOVER_XML_METADATA | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 74b0c33570c9a7f6889e9754eeac7426f72c98ac
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34034656"
---
# <a name="discoverxmlmetadata-rowset"></a>Conjunto de filas DISCOVER_XML_METADATA
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
 La restricción, **ObjectExpansion**, está disponible para todos los objetos principales de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. El cliente normalmente usa las restricciones para describir los objetos OLAP para los que se va a devolver el DDL y utiliza la restricción **ObjectExpansion** para definir el grado de expansión en el DDL devuelto. En la tabla siguiente indica si se permite el valor de enumeración para [Modificar elemento &#40;XMLA&#41; ](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comandos.  
  
|Valor de enumeración|Description|  
|-----------------------|-----------------|  
|**ReferenceOnly**|Devuelve solamente el nombre, identificador, marca de tiempo y estado requeridos para los objetos solicitados y todos los objetos principales descendientes de forma recursiva.|  
|**ObjectProperties**|Expande el objeto solicitado sin referencias a los objetos contenidos (incluye los objetos secundarios contenidos expandidos).|  
|**ExpandObject**|Igual que *ObjectProperties*, pero también devuelve el nombre, identificador y marca de tiempo de los objetos principales contenidos.|  
|**ExpandFull**|Expande totalmente el objeto solicitado de forma recursiva hasta el final de cada objeto contenido.|  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
