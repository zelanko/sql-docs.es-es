---
title: OLE DB para OLAP Schema Rowsets | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- schema rowsets [Analysis Services], OLE DB for OLAP
- OLE DB for OLAP schema rowsets
- schema rowsets [OLE DB for OLAP]
- rowsets [Analysis Services], OLE DB for OLAP
ms.assetid: 5fad3ecc-407c-4148-862e-ea6119cc7480
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd2e29e03617ccc3929ca0845e2b703e406cbfb2
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48172975"
---
# <a name="ole-db-for-olap-schema-rowsets"></a>OLE DB para los conjuntos de filas de esquema OLAP
  El proveedor [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) admite las siguientes DB OLE para conjuntos de filas de esquema OLAP.  
  
> [!NOTE]  
>  Para comprobar si un proveedor de origen de datos determinado admite un conjunto de filas, use el `DISCOVER_ENUMERATIONS` conjunto de filas con el [Discover](../../xmla/xml-elements-methods-discover.md) método.  
  
 También puede encontrar información detallada acerca de estos conjuntos de filas buscando el tema "OLAP Schema Rowsets", en MSDN Library en este [sitio Web de Microsoft](http://go.microsoft.com/fwlink/?LinkId=15426).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Conjunto de filas de esquema<sup>1</sup>|Descripción|  
|-------------------------------|-----------------|  
|[Conjunto de filas DISCOVER_INSTANCES](discover-instances-rowset.md)|Describe las instancias en el servidor.|  
|[Conjunto de filas DISCOVER_KEYWORDS &#40;OLE DB para OLAP&#41;](discover-keywords-rowset-ole-db-for-olap.md)|Enumera una lista de palabras reservada por el proveedor.|  
|[Conjunto de filas MDSCHEMA_ACTIONS](mdschema-actions-rowset.md)|Describe las acciones que pueden estar disponibles para la aplicación cliente.|  
|[Conjunto de filas MDSCHEMA_CUBES](mdschema-cubes-rowset.md)|Describe la estructura de cubos dentro de una base de datos.|  
|[Conjunto de filas MDSCHEMA_DIMENSIONS](mdschema-dimensions-rowset.md)|Describe las dimensiones compartidas y privadas dentro de una base de datos.|  
|[Conjunto de filas MDSCHEMA_FUNCTIONS](mdschema-functions-rowset.md)|Describe las funciones que están disponibles para las aplicaciones cliente conectadas a la base de datos.|  
|[Conjunto de filas MDSCHEMA_HIERARCHIES](mdschema-hierarchies-rowset.md)|Describe cada jerarquía contenida en una dimensión determinada.|  
|[Conjunto de filas MDSCHEMA_INPUT_DATASOURCES](mdschema-input-datasources-rowset.md)|Describe los orígenes de datos definidos dentro de la base de datos.|  
|[Conjunto de filas MDSCHEMA_KPIS](mdschema-kpis-rowset.md)|Describe los indicadores clave de rendimiento (KPI) incluidos en una base de datos.|  
|[Conjunto de filas MDSCHEMA_LEVELS](mdschema-levels-rowset.md)|Describe cada nivel dentro de una jerarquía determinada.|  
|[Conjunto de filas MDSCHEMA_MEASUREGROUP_DIMENSIONS](mdschema-measuregroup-dimensions-rowset.md)|Enumera las dimensiones de grupos de medida.|  
|[Conjunto de filas MDSCHEMA_MEASUREGROUPS](mdschema-measuregroups-rowset.md)|Describe los grupos de medida dentro de una base de datos.|  
|[Conjunto de filas MDSCHEMA_MEASURES](mdschema-measures-rowset.md)|Describe cada medida dentro de en un cubo.|  
|[Conjunto de filas MDSCHEMA_MEMBERS](mdschema-members-rowset.md)|Describe los miembros incluidos en una base de datos.|  
|[Conjunto de filas MDSCHEMA_PROPERTIES](mdschema-properties-rowset.md)|Describe las propiedades de los miembros dentro de una base de datos.|  
|[Conjunto de filas MDSCHEMA_SETS](mdschema-sets-rowset.md)|Describe los conjuntos definidos actualmente en una base de datos, incluidos los conjuntos de ámbito de sesión.|  
  
 <sup>1</sup> todos los conjuntos de filas de esquema enumerados aquí son compatibles con el proveedor de origen de datos MSOLAP para el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] proveedor XMLA.  
  
## <a name="see-also"></a>Vea también  
 [Conjunto de filas DISCOVER_ENUMERATORS](../xml/discover-enumerators-rowset.md)   
 [Conjuntos de filas de esquema de Analysis Services](../../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
