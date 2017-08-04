---
title: IsTestCase (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IsTestCase
dev_langs:
- DMX
helpviewer_keywords:
- IsTestCase function
ms.assetid: 7ff4b895-9bb4-4e26-ab1b-c9049cfc2291
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0880841c201e9f25eb4685d0e6368abbb5bca885
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Indica si un caso se utiliza como un caso de prueba para la estructura o modelo de minería de datos especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>Tipo de resultado  
 Devuelve **true** si el caso forma parte del conjunto de datos de prueba; en caso contrario, **false**.  
  
## <a name="remarks"></a>Comentarios  
 Si utiliza el Asistente para minería de datos con el fin de crear una estructura de minería de datos y el modelo de minería de datos relacionado, de forma predeterminada, el 30 por ciento de los casos se reservan para utilizarse como conjunto de datos de prueba. Los casos restantes se usan para entrenar el modelo de minería de datos. El mismo conjunto de datos de prueba se puede utilizar con todos los modelos que se basan en esa estructura. Sin embargo, si utiliza DMX para crear el modelo de minería de datos, de forma predeterminada, todos los datos se utilizan para entrenar el modelo y no se crea ningún conjunto de prueba. Para habilitar la creación de un conjunto de datos de prueba, debe establecer los parámetros de la cláusula WITH HOLDOUT.  
  
 Puede determinar si un conjunto de prueba se ha creado en una estructura de minería de datos específica viendo el valor de las propiedades <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> y <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A>.  
  
> [!NOTE]  
>  Obtención de detalles debe habilitarse en el modelo si desea utilizar las funciones IsTrainingCase o IsTestCase para devolver detalles sobre los casos en un modelo determinado. Para obtener más información, vea [Habilitar la obtención de detalles para un modelo de minería](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md).  
  
 Para devolver casos que forman parte del conjunto de datos de entrenamiento, utilice la función [IsTrainingCase &#40; DMX &#41;](../dmx/istrainingcase-dmx.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el `Targeted Mailing` estructura de minería de datos que se crea en el [Tutorial básico de minería de datos](http://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). La consulta devuelve todos los casos de la estructura que se utilizan para pruebas.  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 Para obtener más información acerca de cómo consultar los casos que se usan en la minería de datos, vea [SELECT FROM &#60; modelo &#62;. CASOS &#40; DMX &#41; ](../dmx/select-from-model-cases-dmx.md) y [SELECT FROM &#60; estructura &#62;. CASOS](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40; DMX &#41;](../dmx/functions-dmx.md)   
 [Consultas de minería de datos](../analysis-services/data-mining/data-mining-queries.md)   
 [Conjuntos de datos de aprendizaje y prueba](../analysis-services/data-mining/training-and-testing-data-sets.md)  
  
  

