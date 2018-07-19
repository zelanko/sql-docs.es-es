---
title: SELECT FROM &lt;modelo&gt;. SAMPLE_CASES (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f4443f05fbee790f5f1d266f451e1105b9c00197
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37992047"
---
# <a name="select-from-ltmodelgtsamplecases-dmx"></a>SELECT FROM &lt;modelo&gt;. SAMPLE_CASES (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve ejemplos de casos que son representativos de los casos que se emplean para entrenar el modelo de minería de datos.  
  
 Para poder utilizar esta instrucción, debe habilitar la obtención de detalles al crear el modelo de minería de datos. Para obtener más información acerca de cómo habilitar la obtención de detalles, consulte [CREATE MINING MODEL &#40;DMX&#41;](../dmx/create-mining-model-dmx.md), [SELECT INTO &#40;DMX&#41;](../dmx/select-into-dmx.md), y [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
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
  
## <a name="remarks"></a>Notas  
 Pueden generarse casos de ejemplo que podrían no existir en los datos de entrenamiento. El caso devuelto es representativo del nodo de contenido especificado.  
  
 Aunque el [!INCLUDE[msCoName](../includes/msconame-md.md)] es el único algoritmo de clústeres de secuencia [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmo que admite el uso de SELECT FROM \<modelo >. SAMPLE_CASES, algoritmos de terceros también podrían admitirlo.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se devuelven casos de ejemplo que sirven para entrenar el modelo de minería de datos Target Mail. Mediante el [IsInNode &#40;DMX&#41; ](../dmx/isinnode-dmx.md) funcionando en el **donde** cláusula devuelve exclusivamente casos asociados con el nodo '000000003'. La cadena de nodo se encuentra en la columna NODE_UNIQUE_NAME del conjunto de filas de esquema.  
  
```  
Select * from [Sequence Clustering].SAMPLE_Cases  
WHERE IsInNode('000000003')  
```  
  
## <a name="see-also"></a>Vea también  
 [SELECCIONE &AMP;#40;DMX&AMP;#41;](../dmx/select-dmx.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
