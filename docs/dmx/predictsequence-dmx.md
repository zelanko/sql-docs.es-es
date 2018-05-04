---
title: PredictSequence (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- PredictSequence
dev_langs:
- DMX
helpviewer_keywords:
- PredictSequence function
ms.assetid: c2992dfc-b99d-4430-8dcd-21ad3ffd4590
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: b8ef0b3f0ba361e368695b31d15b26cd013ed6e8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 Si el *n* se especifica el parámetro, devuelve los siguientes valores:  
  
-   Si *n* es mayor que cero, los valores de secuencia más probables en las próximas *n* pasos.  
  
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
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
