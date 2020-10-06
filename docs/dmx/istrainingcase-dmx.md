---
description: IsTrainingCase (DMX)
title: IsTrainingCase (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5eb68d0aaa0d19fb903154b8d5c4d4135b57883e
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726156"
---
# <a name="istrainingcase-dmx"></a>IsTrainingCase (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Indica si un caso se utiliza como caso de entrenamiento para el modelo o estructura de minería de datos especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
IsTrainingCase()  
```  
  
## <a name="result-type"></a>Tipo de resultado  
 Devuelve **true** si el caso forma parte del conjunto de datos de entrenamiento; en caso contrario, **false**.  
  
## <a name="remarks"></a>Observaciones  
 Si utiliza el Asistente para minería de datos con el fin de crear una estructura de minería de datos y el modelo de minería de datos relacionado, de forma predeterminada, el 30 por ciento de los casos se reservan para utilizarse como conjunto de datos de prueba. Los casos restantes en el origen de datos que se especifica se utilizan para entrenar el modelo. Sin embargo, si se utiliza Extensiones de minería de Datos (DMX) para crear el modelo de minería de datos, de forma predeterminada, todos los datos se utilizan para entrenar el modelo y no se crea ningún conjunto de pruebas. Para habilitar la creación de un conjunto de datos de prueba, se deben establecer los parámetros de la cláusula WITH HOLDOUT.  
  
 Se puede determinar si los datos de una estructura de minería de datos determinada se han dividido en conjuntos de entrenamiento y de prueba observando el valor de las propiedades <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxCases%2A> y <xref:Microsoft.AnalysisServices.MiningStructure.HoldoutMaxPercent%2A>.  
  
> [!NOTE]  
>  La obtención de detalles debe estar habilitada en el modelo si desea utilizar las funciones IsTrainingCase o IsTestCase para devolver detalles sobre los casos del modelo. Para obtener más información, vea [Habilitar la obtención de detalles para un modelo de minería](/analysis-services/data-mining/enable-drillthrough-for-a-mining-model).  
  
 Para devolver los casos que forman parte del conjunto de datos de prueba, use la función [IsTestCase &#40;DMX&#41;](../dmx/istestcase-dmx.md).  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el modelo de minería de datos de agrupación en clústeres del escenario de distribución de datos de destino en el [tutorial básico de minería de datos](/previous-versions/sql/sql-server-2016/ms167167(v=sql.130)). La consulta solo devuelve los casos que se utilizaron para entrenar el modelo de minería de datos. Además, los casos de entrenamiento se restringen a los clientes menores de 40 años.  
  
```  
SELECT *  
FROM [TM Clustering].CASES  
WHERE IsTrainingCase()  
AND [Age] <40  
```  
  
 Para ver otros ejemplos de cómo consultar los casos que se usan en la minería de datos, vea [SELECT FROM &#60;model&#62;. Los casos &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md) y [seleccionar de &#60;estructura&#62;. CASOS](../dmx/select-from-structure-cases.md).  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de datos de entrenamiento y de prueba](/analysis-services/data-mining/training-and-testing-data-sets)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Consultas de minería de datos](/analysis-services/data-mining/data-mining-queries)  
  
