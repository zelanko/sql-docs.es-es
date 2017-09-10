---
title: Elemento AggregationPrefix (ASSL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AggregationPrefix Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationPrefix
helpviewer_keywords:
- AggregationPrefix element
ms.assetid: 1581e0df-ae8e-41ce-9c92-f0f7cac487f2
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8ef1688e23bddf1136775474c93ae62a05bb97ab
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="aggregationprefix-element-assl"></a>Elemento AggregationPrefix (ASSL)
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
 [Propiedades &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
