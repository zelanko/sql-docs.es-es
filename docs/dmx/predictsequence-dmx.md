---
title: PredictSequence (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 09911d0d0d8553ab26d0fc141bcc07ed2f479728
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83666971"
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
  
## <a name="return-type"></a>Tipo de valor devuelto  
 \<> una expresión de tabla.  
  
## <a name="remarks"></a>Observaciones  
 Si se especifica el parámetro *n* , devuelve los valores siguientes:  
  
-   Si *n* es mayor que cero, los valores de secuencia más probables en los siguientes *n* pasos.  
  
-   Si se especifican *n-Start* y *n-end* , los valores de secuencia de *n-Start* a *n-end*.  
  
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve una secuencia de los cinco productos que es más probable que un cliente de la base de datos [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] compre en función del modelo de minería de datos Sequence Clustering.  
  
```  
SELECT  
  PredictSequence([Sequence Clustering].[v Assoc Seq Line Items],5)  
From  
  [Sequence Clustering]  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
