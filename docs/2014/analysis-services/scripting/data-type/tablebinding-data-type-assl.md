---
title: Tipo de datos TableBinding (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TableBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TableBinding
helpviewer_keywords:
- TableBinding data type
ms.assetid: 3195dca4-82bf-46b7-a31f-5383586e3573
caps.latest.revision: 39
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 475044a0bcad3c90ffaffa71eeeb6735a37f96c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220255"
---
# <a name="tablebinding-data-type-assl"></a>Tipo de datos TableBinding (ASSL)
  Define un tipo de datos derivado que representa un enlace con una tabla.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<TableBinding>  
   <!-- The following elements extend TabularBinding -->  
   <DataSourceID>...</DataSourceID>  
   <DbTableName>...</DbTableName>  
   <DbSchemaName>...</DbSchemaName>  
</TableBinding>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[TabularBinding](binding-data-type-assl.md)|  
|Tipos de datos derivados|None|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|None|  
|Elementos secundarios|[DataSourceID](../properties/id-element-assl.md), [DbSchemaName](../properties/name-element-assl.md), [DbTableName](../properties/dbtablename-element-assl.md)|  
|Elementos derivados|Consulte [enlace](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Notas  
 Tenga en cuenta que la referencia a otras tablas en la expresión de filtro mediante subselect puede afectar al rendimiento de algunos orígenes de datos. Sin embargo, el diseñador puede controlar totalmente la expresión de SQL definiendo una consulta con nombre en la vista del origen de datos y, a continuación, haciendo referencia a ella.  
  
 El método de definición de enlaces para una partición es independiente del uso de tablas con particiones en la vista del origen de datos.  
  
 Considere, por ejemplo, un grupo de medidas cuya tabla predeterminada es "Sales", con las columnas Date, Product ID, Qty, Price y Amount (calculadas en la vista del origen de datos). A continuación, la partición "Sales97" podría usar la tabla "Sales97" con filtro " Year(Sales.Date) = 97."  
  
 La consulta efectiva es:  
  
```  
SELECT Date, Product ID, Qty, Price, Qty * Price AS Amount   
   FROM Sales97 As Sales  
   WHERE Year(Sales.Date) = 97  
```  
  
 La expresión calculada todavía es válida, aunque la expresión haya usado nombres de tabla calificados (por ejemplo, Sales.Qty). Lo mismo sucede si la tabla se sustituye por alguna consulta "SELECT…" La cláusula FROM anterior se convertiría en "FROM SELECT... As Sales."  
  
 Para obtener más información sobre la `Binding` tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) del tipo `Binding` y la jerarquía de herencia de `Binding` tipos, vea [tipo de datos de enlace &#40;ASSL&#41;](binding-data-type-assl.md).  
  
 Para obtener información general de los enlaces de datos en ASSL, vea [orígenes de datos y enlaces &#40;Multidimensional de SSAS&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.TableBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de datos Binding &#40;ASSL&#41;](binding-data-type-assl.md)   
 [Orígenes de datos y enlaces &#40;SSAS Multidimensional&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Tipos de datos XML de lenguaje Scripting de Analysis Services &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
