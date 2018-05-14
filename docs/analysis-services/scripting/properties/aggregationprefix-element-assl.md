---
title: Elemento AggregationPrefix (ASSL) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b23721728f8e196c47ab326024a6f514631c3b6f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="aggregationprefix-element-assl"></a>Elemento AggregationPrefix (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define el prefijo común que se va a utilizar para los nombres de la agregación en el elemento primario asociado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Cube> <!-- or Database, MeasureGroup, Partition -->  
   ...  
   <AggregationPrefix>...</AggregationPrefix>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Cadena|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cubo](../../../analysis-services/scripting/objects/cube-element-assl.md), [base de datos](../../../analysis-services/scripting/objects/database-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [partición](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Prefijos de agregación generan nombres en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]y también generar los nombres de tabla en la base de datos relacional para las agregaciones almacenadas en una partición de OLAP (ROLAP) relacional.  
  
 Un nombre de agregación totalmente expandido está formado por las siguientes partes:  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 Las primeras cuatro partes del nombre de agregación conforman el prefijo de agregación. El usuario proporciona las primeras cuatro partes:  
  
-   *DatabasePrefix* representa el valor de la **AggregationPrefix** elemento asociado con un **base de datos** elemento.  
  
-   *CubePrefix* representa el valor de la **AggregationPrefix** elemento asociado con un **cubo** elemento.  
  
-   *MeasureGroupPrefix* representa el valor de la **AggregationPrefix** elemento asociado con un **MeasureGroup** elemento.  
  
-   *PartitionPrefix* representa el valor de la **AggregationPrefix** elemento asociado con un **partición** elemento.  
  
 La quinta parte del nombre, *AggregationID*, es un identificador definido por el sistema y los usuarios no tienen ningún control sobre esta parte del nombre.  
  
 Los elementos que corresponden a los elementos primarios de **AggregationPrefix** en el modelo de objetos de Analysis Management Objects (AMO) son <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.MeasureGroup>, y <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
