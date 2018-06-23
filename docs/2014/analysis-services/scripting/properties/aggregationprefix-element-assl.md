---
title: Elemento AggregationPrefix (ASSL) | Documentos de Microsoft
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
- AggregationPrefix Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AggregationPrefix
helpviewer_keywords:
- AggregationPrefix element
ms.assetid: 1581e0df-ae8e-41ce-9c92-f0f7cac487f2
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 84f7b086e1cdc2516f0912a4580d0b3eb45132ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203512"
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
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Cubo](../objects/cube-element-assl.md), [base de datos](../objects/database-element-assl.md), [MeasureGroup](../objects/group-element-assl.md), [partición](../objects/partition-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Prefijos de agregación generan nombres en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]y también generar los nombres de tabla en la base de datos relacional para las agregaciones almacenadas en una partición de OLAP (ROLAP) relacional.  
  
 Un nombre de agregación totalmente expandido está formado por las siguientes partes:  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 Las primeras cuatro partes del nombre de agregación conforman el prefijo de agregación. El usuario proporciona las primeras cuatro partes:  
  
-   *DatabasePrefix* representa el valor de la `AggregationPrefix` elemento asociado con un `Database` elemento.  
  
-   *CubePrefix* representa el valor de la `AggregationPrefix` elemento asociado con un `Cube` elemento.  
  
-   *MeasureGroupPrefix* representa el valor de la `AggregationPrefix` elemento asociado con un `MeasureGroup` elemento.  
  
-   *PartitionPrefix* representa el valor de la `AggregationPrefix` elemento asociado con un `Partition` elemento.  
  
 La quinta parte del nombre, *AggregationID*, es un identificador definido por el sistema y los usuarios no tienen ningún control sobre esta parte del nombre.  
  
 Los elementos que corresponden a los elementos primarios de `AggregationPrefix` en el modelo de objetos de Objetos de administración de análisis (AMO) son <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.MeasureGroup> y <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  