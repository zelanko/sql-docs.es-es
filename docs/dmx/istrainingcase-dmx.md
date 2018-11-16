---
title: IsTrainingCase (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c42ecb976884573e313c06adc4241e202e123df
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51599936"
---
# <a name="istrainingcase-dmx"></a>IsTrainingCase (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Indica si un caso se utiliza como caso de entrenamiento para el modelo o estructura de minería de datos especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>Tipo de resultado  
 Devuelve **true** si el caso forma parte del conjunto de datos de entrenamiento; de lo contrario **false**.  
  
## <a name="remarks"></a>Comentarios  
 Si utiliza el Asistente para minería de datos con el fin de crear una estructura de minería de datos y el modelo de minería de datos relacionado, de forma predeterminada, el 30 por ciento de los casos se reservan para utilizarse como conjunto de datos de prueba. Los casos restantes en el origen de datos que se especifica se utilizan para entrenar el modelo. Sin embargo, si se utiliza Extensiones de minería de Datos (DMX) para crear el modelo de minería de datos, de forma predeterminada, todos los datos se utilizan para entrenar el modelo y no se crea ningún conjunto de pruebas. Para habilitar la creación de un conjunto de datos de prueba, se deben establecer los parámetros de la cláusula WITH HOLDOUT.  
  
 Se puede determinar si los datos de una estructura de minería de datos determinada se han dividido en conjuntos de entrenamiento y de prueba observando el valor de las propiedades <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> y <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A>.  
  
> [!NOTE]  
>  Obtención de detalles debe habilitarse en el modelo si desea utilizar las funciones IsTrainingCase o IsTestCase para devolver detalles sobre los casos del modelo. Para obtener más información, vea [Habilitar la obtención de detalles para un modelo de minería](../analysis-services/data-mining/enable-drillthrough-for-a-mining-model.md).  
  
 Para devolver casos que forman parte del conjunto de datos de prueba, use la función [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el modelo de minería de datos agrupación en clústeres en el escenario de distribución de correo directo en el [Basic Data Mining Tutorial](https://msdn.microsoft.com/library/6602edb6-d160-43fb-83c8-9df5dddfeb9c). La consulta solo devuelve los casos que se utilizaron para entrenar el modelo de minería de datos. Además, los casos de entrenamiento se restringen a los clientes menores de 40 años.  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 Para obtener ejemplos de cómo consultar los casos usados en la minería de datos, vea [SELECT FROM &#60;modelo&#62;. CASOS &#40;DMX&#41; ](../dmx/select-from-model-cases-dmx.md) y [SELECT FROM &#60;estructura&#62;. CASOS](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>Vea también  
 [Entrenamiento y conjuntos de datos de prueba](../analysis-services/data-mining/training-and-testing-data-sets.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Consultas de minería de datos](../analysis-services/data-mining/data-mining-queries.md)  
  
  
