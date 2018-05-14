---
title: Tipo de datos TableBinding (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 80055d443f0a08b7cc957d5fa26d458178d3a1f6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="tablebinding-data-type-assl"></a>Tipo de datos TableBinding (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|Tipos de datos base|[TabularBinding](../../../analysis-services/scripting/data-type/tabularbinding-data-type-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[DataSourceID](../../../analysis-services/scripting/properties/datasourceid-element-assl.md), [DbSchemaName](../../../analysis-services/scripting/properties/dbschemaname-element-assl.md), [DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)|  
|Elementos derivados|Vea [Binding](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Comentarios  
 Tenga en cuenta que la referencia a otras tablas en la expresión de filtro mediante subselect puede afectar al rendimiento de algunos orígenes de datos. Sin embargo, el diseñador puede controlar totalmente la expresión de SQL definiendo una consulta con nombre en la vista del origen de datos y, a continuación, haciendo referencia a ella.  
  
 El método de definición de enlaces para una partición es independiente del uso de tablas con particiones en la vista del origen de datos.  
  
 Considere, por ejemplo, un grupo de medidas cuya tabla predeterminada es "Sales", con las columnas Date, Product ID, Qty, Price y Amount (calculadas en la vista del origen de datos). A continuación, la partición "Sales97" podría usar la tabla "Sales97" con filtro " Year(Sales.Date) = 97."  
  
 La consulta efectiva es:  
  
```  
SELECT Date, Product ID, Qty, Price, Qty * Price AS Amount   
   FROM Sales97 As Sales  
   WHERE Year(Sales.Date) = 97  
```  
  
 La expresión calculada todavía es válida, aunque la expresión haya usado nombres de tabla calificados (por ejemplo, Sales.Qty). Lo mismo se aplica si en su lugar, la tabla se sustituye por alguna consulta "SELECT..." La cláusula FROM anterior se convertiría en "FROM SELECT... As Sales."  
  
 Para obtener más información sobre la **enlace** tipo, incluidas las tablas de objetos de Analysis Services Scripting Language (ASSL) del tipo **enlace** y la jerarquía de herencia de **deenlace** tipos, consulte [tipo de datos de enlace &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 Para obtener información general de enlaces de datos en ASSL, vea [orígenes de datos y enlaces & #40; SSAS Multidimensional & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.TableBinding>.  
  
## <a name="see-also"></a>Vea también  
 [Tipo de enlace de datos & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)   
 [Orígenes de datos y enlaces &#40;SSAS Multidimensional&#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)   
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
