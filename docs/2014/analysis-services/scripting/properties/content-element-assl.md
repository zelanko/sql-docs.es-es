---
title: (ASSL) del elemento de contenido | Microsoft Docs
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
- Content Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Content
helpviewer_keywords:
- Content element
ms.assetid: 221addef-2f88-49c5-b8f5-9eee330497a9
caps.latest.revision: 42
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bd9e3c237d8009ac153e8c69033ce9cce958aba3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267481"
---
# <a name="content-element-assl"></a>Elemento Content (ASSL)
  Describe el contenido de la columna en la [MiningStructure](../objects/miningstructure-element-assl.md) elemento.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ScalarMiningStructureColumn>  
   ...  
   <Content>...</Content>  
   ...  
</ScalarMiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento requerido que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[ScalarMiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 Esta enumeración describe el tipo de contenido representado por una columna de estructura de minería de datos y se puede extender según sea necesario minando los proveedores del algoritmo. Para obtener más información sobre los tipos de contenido, vea [Tipos de contenido &#40;minería de datos&#41;](../../data-mining/content-types-data-mining.md).  
  
 Todos los proveedores de algoritmo de minería de datos admiten normalmente los valores enumerados en la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Discretos*|La columna contiene valores discretos.|  
|*Continua*|Los valores para la columna definen un conjunto continuo de datos numéricos.|  
|*Datos discretos*|Los valores de la columna representan grupos (o depósitos) de valores que se derivan de una columna continua.|  
|*Ordenada*|Los valores de la columna definen un conjunto ordenado.|  
|*Cíclica*|Los valores de la columna definen un conjunto ordenado cíclico.|  
|*Probabilidad*|Los valores de la columna especifican una probabilidad para las columnas contenidas en el [ClassifiedColumns](../collections/columns-element-assl.md) elemento primario `ScalarMiningStructureColumn`.|  
|*Variance*|Los valores de la columna especifican una varianza para las columnas contenidas en el elemento `ClassifiedColumns` del elemento primario `ScalarMiningStructureColumn`.|  
|*StdDev*|Los valores de la columna especifican una desviación estándar para las columnas contenidas en el elemento `ClassifiedColumns` del elemento primario `ScalarMiningStructureColumn`.|  
|*ProbabilityVariance*|Los valores de la columna especifican una probabilidad para las columnas contenidas en el elemento `ClassifiedColumns` del elemento primario `ScalarMiningStructureColumn`.|  
|*ProbabilityStdDev*|Los valores de la columna especifican una desviación estándar para las columnas contenidas en el `ClassifiedColumns` del elemento primario `ScalarMiningStructureColumn`.|  
|*Soporte técnico*|Los valores de la columna especifican información de compatibilidad para las columnas contenidas en el elemento `ClassifiedColumns` del elemento primario `ScalarMiningStructureColumn`. **Nota:** esta columna se proporciona como parte de la norma para proveedores de algoritmos de minería de datos de terceros. **Nota:** Microsoft proporciona algoritmos no tienen ningún uso para esta columna. <br /><br /> .|  
|*Key*|La columna es una columna de clave. **Nota:** este tipo de contenido solo es aplicable a las columnas de clave, en el que el `IsKey` elemento está establecido en `True`.|  
  
 Además de estos valores no estándar, incluidos con los proveedores de algoritmos de minería de datos [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admiten los valores de la tabla siguiente.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*Secuencia de teclas*|La columna es una columna de clave y los valores de la columna representan una secuencia de eventos. **Nota:** este tipo de contenido solo es aplicable a las columnas de clave, en el que el `IsKey` elemento está establecido en `True`.|  
|*Clave temporal*|La columna es una columna de clave y los valores de la columna representan unidades de medida de tiempo. **Nota:** este tipo de contenido solo es aplicable a las columnas de clave, en el que el `IsKey` elemento está establecido en `True`.|  
|*Secuencia*|Los valores de la columna representan un flujo de eventos.|  
|*Time*|Los valores para la columna representan las unidades de medida de tiempo.|  
  
 La enumeración que corresponde a los valores permitidos de `Content` en el modelo de objetos Objetos de administración de análisis (AMO) es <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>.  
  
## <a name="see-also"></a>Vea también  
 [Elemento ClassifiedColumns &#40;ASSL&#41;](../collections/columns-element-assl.md)   
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
