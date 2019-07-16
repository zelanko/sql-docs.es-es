---
title: PredictSequence (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c6828b77af36b5dbbc50fbca0210961a7f2ed20c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68041924"
---
# <a name="predictsequence-dmx"></a>PredictSequence (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Predice valores de secuencia futuros para un conjunto de datos de secuencia especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PredictSequence(<table column reference>)  
PredictSequence(\<table column reference, n>)  
PredictSequence(\<table column reference, n-start, n-end>)  
```  
  
## <a name="return-type"></a>Tipo devuelto  
 Un \<expresión de tabla >.  
  
## <a name="remarks"></a>Comentarios  
 Si el *n* parámetro se especifica, devuelve los valores siguientes:  
  
-   Si *n* es mayor que cero, los valores de secuencia más probable es que en los próximos *n* pasos.  
  
-   Si ambos *n-start* y *n-end* se especifican, los valores de secuencia de *n-start* a *n-end*.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve una secuencia de los cinco productos que es más probable que un cliente de la base de datos [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] compre en función del modelo de minería de datos Sequence Clustering.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
