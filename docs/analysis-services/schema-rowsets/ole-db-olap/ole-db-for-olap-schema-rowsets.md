---
title: OLE DB para OLAP Schema Rowsets | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a8e3413b951cb12796139c3ff390a2d1951c02ab
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="ole-db-for-olap-schema-rowsets"></a>OLE DB para los conjuntos de filas de esquema OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  El proveedor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) admite las siguientes DB OLE para conjuntos de filas de esquema OLAP.  
  
> [!NOTE]  
>  Para comprobar si un proveedor de origen de datos determinado admite un conjunto de filas, utilice la **DISCOVER_ENUMERATIONS** conjunto de filas con el [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.  
  
 También puede encontrar información detallada acerca de estos conjuntos de filas buscando el tema "OLAP Schema Rowsets", en MSDN Library en este [sitio Web de Microsoft](http://go.microsoft.com/fwlink/?LinkId=15426).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Conjunto de filas de esquema<sup>1</sup>|Description|  
|-------------------------------|-----------------|  
|[Conjunto de filas DISCOVER_INSTANCES](../../../analysis-services/schema-rowsets/ole-db-olap/discover-instances-rowset.md)|Describe las instancias en el servidor.|  
|[Conjunto de filas DISCOVER_KEYWORDS & #40; OLE DB para OLAP & #41;](../../../analysis-services/schema-rowsets/ole-db-olap/discover-keywords-rowset-ole-db-for-olap.md)|Enumera una lista de palabras reservada por el proveedor.|  
|[Conjunto de filas MDSCHEMA_ACTIONS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)|Describe las acciones que pueden estar disponibles para la aplicación cliente.|  
|[Conjunto de filas MDSCHEMA_CUBES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|Describe la estructura de cubos dentro de una base de datos.|  
|[Conjunto de filas MDSCHEMA_DIMENSIONS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|Describe las dimensiones compartidas y privadas dentro de una base de datos.|  
|[Conjunto de filas MDSCHEMA_FUNCTIONS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)|Describe las funciones que están disponibles para las aplicaciones cliente conectadas a la base de datos.|  
|[Conjunto de filas MDSCHEMA_HIERARCHIES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|Describe cada jerarquía contenida en una dimensión determinada.|  
|[Conjunto de filas MDSCHEMA_INPUT_DATASOURCES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)|Describe los orígenes de datos definidos dentro de la base de datos.|  
|[Conjunto de filas MDSCHEMA_KPIS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|Describe los indicadores clave de rendimiento (KPI) incluidos en una base de datos.|  
|[Conjunto de filas MDSCHEMA_LEVELS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|Describe cada nivel dentro de una jerarquía determinada.|  
|[Conjunto de filas MDSCHEMA_MEASUREGROUP_DIMENSIONS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)|Enumera las dimensiones de grupos de medida.|  
|[Conjunto de filas MDSCHEMA_MEASUREGROUPS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)|Describe los grupos de medida dentro de una base de datos.|  
|[Conjunto de filas MDSCHEMA_MEASURES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|Describe cada medida dentro de en un cubo.|  
|[Conjunto de filas MDSCHEMA_MEMBERS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|Describe los miembros incluidos en una base de datos.|  
|[Conjunto de filas MDSCHEMA_PROPERTIES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|Describe las propiedades de miembros dentro de una base de datos.|  
|[Conjunto de filas MDSCHEMA_SETS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|Describe los conjuntos definidos actualmente en una base de datos, incluidos los conjuntos de ámbito de sesión.|  
  
 <sup>1</sup> todos los conjuntos de filas de esquema enumerados aquí son compatibles con el proveedor de origen de datos MSOLAP para el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] proveedor XMLA.  
  
## <a name="see-also"></a>Vea también  
 [Conjunto de filas DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Conjuntos de filas de esquema de Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
