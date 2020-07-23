---
title: FORMA (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4d5d93d4236b3cf86719c416ba87517401e4b4f5
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970312"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;consulta de datos &gt; de origen-forma
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Combina consultas de varios orígenes de datos en una única tabla jerárquica (es decir, una tabla con tablas anidadas), que se convierte en la tabla de caso para el modelo de minería de datos.  
  
 La sintaxis completa del comando **forma** está documentada en el [!INCLUDE[msCoName](../includes/msconame-md.md)] Kit de desarrollo de software (SDK) de componentes de acceso a datos (MDAC).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SHAPE {<primary query>}  
APPEND ({ <child table query> }   
     RELATE <primary column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <primary column> TO <child column>)   
          AS < column table name>  
...  
]       
```  
  
## <a name="arguments"></a>Argumentos  
 *consulta principal*  
 Consulta que devuelve la tabla primaria.  
  
 *consulta de tabla secundaria*  
 Consulta que devuelve la tabla anidada.  
  
 *columna principal*  
 Columna de la tabla primaria que sirve para identificar filas secundarias a partir del resultado de una consulta de tabla secundaria.  
  
 *columna secundaria*  
 Columna de la tabla secundaria que identifica la fila primaria del resultado de una consulta primaria.  
  
 *nombre de la tabla de columnas*  
 Nombre de columna que se acaba de anexar en la tabla primaria para la tabla anidada.  
  
## <a name="remarks"></a>Observaciones  
 Debe ordenar las consultas por la columna que relaciona la tabla primaria con la tabla secundaria.  
  
## <a name="examples"></a>Ejemplos  
 Puede utilizar el ejemplo siguiente en una instrucción [INSERT INTO &#40;DMX&#41;](../dmx/insert-into-dmx.md) para entrenar un modelo que contenga una tabla anidada. Las dos tablas de la instrucción **Shape** se relacionan a través de la columna **OrderNumber** .  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>Consulte también  
 [&#60;consulta de datos de origen&#62;](../dmx/source-data-query.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
