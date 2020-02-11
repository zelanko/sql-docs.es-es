---
title: IsTestCase (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 050ceeaa8eb5700f108b7135616817e09c0031cb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68889038"
---
# <a name="istestcase-dmx"></a>IsTestCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica si un caso se utiliza como un caso de prueba para la estructura o modelo de minería de datos especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsTestCase()  
```  
  
## <a name="result-type"></a>Tipo de resultado  
 Devuelve **true** si el caso forma parte del conjunto de datos de prueba; en caso contrario, **false**.  
  
## <a name="remarks"></a>Observaciones  
 Si utiliza el Asistente para minería de datos con el fin de crear una estructura de minería de datos y el modelo de minería de datos relacionado, de forma predeterminada, el 30 por ciento de los casos se reservan para utilizarse como conjunto de datos de prueba. Los casos restantes se usan para entrenar el modelo de minería de datos. El mismo conjunto de datos de prueba se puede utilizar con todos los modelos que se basan en esa estructura. Sin embargo, si utiliza DMX para crear el modelo de minería de datos, de forma predeterminada, todos los datos se utilizan para entrenar el modelo y no se crea ningún conjunto de prueba. Para habilitar la creación de un conjunto de datos de prueba, debe establecer los parámetros de la cláusula WITH HOLDOUT.  
  
 Puede determinar si un conjunto de prueba se ha creado en una estructura de minería de datos específica viendo el valor de las propiedades <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> y <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A>.  
  
> [!NOTE]  
>  La obtención de detalles debe estar habilitada en el modelo si desea utilizar las funciones IsTrainingCase o IsTestCase para devolver detalles sobre los casos de un modelo determinado. Para obtener más información, vea [Habilitar la obtención de detalles para un modelo de minería](https://docs.microsoft.com/analysis-services/data-mining/enable-drillthrough-for-a-mining-model).  
  
 Para devolver los casos que forman parte del conjunto de datos de entrenamiento, utilice la función [IsTrainingCase &#40;DMX&#41;](../dmx/istrainingcase-dmx.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se `Targeted Mailing` utiliza la estructura de minería de datos que se crea en el [tutorial básico de minería de datos](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). La consulta devuelve todos los casos de la estructura que se utilizan para pruebas.  
  
```  
SELECT *  
FROM [Targeted Mailing].CASES  
WHERE IsTestCase()  
```  
  
 Para obtener más información sobre cómo consultar los casos que se usan en la minería de datos, vea [SELECT FROM &#60;model&#62;. Los casos &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md) y [seleccionar de &#60;estructura&#62;. CASOS](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Consultas de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-queries)   
 [Conjuntos de datos de entrenamiento y de prueba](https://docs.microsoft.com/analysis-services/data-mining/training-and-testing-data-sets)  
  
  
