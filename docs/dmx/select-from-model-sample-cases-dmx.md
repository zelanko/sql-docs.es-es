---
title: Seleccione del &lt; modelo &gt; . SAMPLE_CASES (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7eda9b0e13ee5cbf918d80f41b9a517906a56a57
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970519"
---
# <a name="select-from-ltmodelgtsample_cases-dmx"></a>Seleccione del &lt; modelo &gt; . SAMPLE_CASES (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Devuelve ejemplos de casos que son representativos de los casos que se emplean para entrenar el modelo de minería de datos.  
  
 Para poder utilizar esta instrucción, debe habilitar la obtención de detalles al crear el modelo de minería de datos. Para obtener más información acerca de cómo habilitar la obtención de detalles, vea [Create Mining MODEL &#40;dmx&#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md)y [ALTER Mining Structure &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT [FLATTENED] [TOP <n>] <expression list> FROM <model>.SAMPLE_CASES  
[WHERE <condition list>] ORDER BY <expression> [DESC|ASC]]  
```  
  
## <a name="arguments"></a>Argumentos  
 *n*  
 Opcional. Entero que especifica el número de filas que se devuelven.  
  
 *lista de expresiones*  
 Lista delimitada por comas de identificadores de columna relacionados.  
  
 *model*  
 Identificador de modelo.  
  
 *lista de condiciones*  
 Opcional. Condiciones para restringir los valores que devuelve la lista de columnas.  
  
 *expression*  
 Opcional. Expresión que devuelve un valor escalar.  
  
## <a name="remarks"></a>Observaciones  
 Pueden generarse casos de ejemplo que podrían no existir en los datos de entrenamiento. El caso devuelto es representativo del nodo de contenido especificado.  
  
 Aunque el [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo de clústeres de secuencia es el único [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo que admite el uso de Select from \<model> . SAMPLE_CASES, los algoritmos de terceros también pueden admitirlo.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelven casos de ejemplo que sirven para entrenar el modelo de minería de datos Target Mail. El uso de la función [IsInNode &#40;DMX&#41;](../dmx/isinnode-dmx.md) en la cláusula **Where** solo devuelve los casos que están asociados al nodo ' 000000003 '. La cadena de nodo se encuentra en la columna NODE_UNIQUE_NAME del conjunto de filas de esquema.  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>Consulte también  
 [SELECCIONE &#40;DMX&#41;](../dmx/select-dmx.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
