---
title: UPDATE (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: UPDATE
dev_langs: DMX
helpviewer_keywords:
- NODE_CAPTION column
- mining models [Analysis Services], content changes
- modifying mining model content
- UPDATE statement [SQL Server], DMX
ms.assetid: 8a2b0942-c490-410c-b1cf-ff2e0fd8e24b
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 64c09a11d988611ec1743f32f9f3724b1df930d1
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="update-dmx"></a>UPDATE (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Cambios de la **NODE_CAPTION** columna en el modelo de minería de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
UPDATE <model>.CONTENT  
SET NODE_CAPTION='new caption'  
[WHERE <condition expression>]  
```  
  
## <a name="arguments"></a>Argumentos  
 *model*  
 Identificador de modelo.  
  
 *nuevo título*  
 Una cadena que contiene el nuevo nombre para el **NODE_CAPTION** columna.  
  
 *expresión de condición*  
 Opcional. Condición para restringir los valores que devuelve la lista de columnas.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente, la **actualización** instrucción cambia el nombre predeterminado, `Cluster 1`, para clúster `001` por el nombre más descriptivo, `Likely Customers`.  
  
```  
UPDATE [TM Clustering].CONTENT  
SET NODE_CAPTION= 'Likely Customers'  
WHERE NODE_UNIQUE_NAME = '001'  
```  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
