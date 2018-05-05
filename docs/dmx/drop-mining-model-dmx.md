---
title: QUITAR EL MODELO DE MINERÍA DE DATOS (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP_MINING_MODEL
dev_langs:
- DMX
helpviewer_keywords:
- DROP MINING MODEL statement
- deleting mining models
- removing mining models
- dropping mining models
- mining models [Analysis Services], deleting
ms.assetid: 8ff561d0-a526-4712-9fff-11df9f8c45a1
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 59824b126e4297232bc16e731eac2f0ab8dabdcf
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="drop-mining-model-dmx"></a>DROP MINING MODEL (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Elimina un modelo de minería de datos de la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP MINING MODEL <model >  
```  
  
## <a name="arguments"></a>Argumentos  
 *model*  
 Identificador de modelo.  
  
## <a name="examples"></a>Ejemplos  
 El código de ejemplo siguiente quita el modelo de minería de datos NBSample.  
  
```  
DROP MINING MODEL [NBSample]  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; las instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos & #40; DMX & #41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
