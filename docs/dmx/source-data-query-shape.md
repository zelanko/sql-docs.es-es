---
title: SHAPE (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: c928d4c96917479f8c37415d5ebe2db9b7f9eb98
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938114"
---
# <a name="ltsource-data-querygt---shape"></a>&lt;consulta de origen de datos&gt; -forma
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Combina consultas de varios orígenes de datos en una única tabla jerárquica (es decir, una tabla con tablas anidadas), que se convierte en la tabla de caso para el modelo de minería de datos.  
  
 La sintaxis completa de la **forma** comando se documenta en el [!INCLUDE[msCoName](../includes/msconame-md.md)] Kit de desarrollo de Software (SDK) de Data Access Components (MDAC).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SHAPE {<master query>}  
APPEND ({ <child table query> }   
     RELATE <master column> TO <child column>)   
          AS <column table name>  
[  
     ({ <child table query> }   
     RELATE <master column> TO <child column>)   
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
 Columna de la tabla secundaria que sirve para identificar la fila primaria a partir del resultado de una consulta de la base de datos maestra.  
  
 *nombre de la tabla de columna*  
 Nombre de columna que se acaba de anexar en la tabla primaria para la tabla anidada.  
  
## <a name="remarks"></a>Comentarios  
 Debe ordenar las consultas por la columna que relaciona la tabla primaria con la tabla secundaria.  
  
## <a name="examples"></a>Ejemplos  
 Puede usar el siguiente ejemplo en un [INSERT INTO &#40;DMX&#41; ](../dmx/insert-into-dmx.md) instrucción para entrenar un modelo que contiene una tabla anidada. Las dos tablas de la **forma** instrucción están relacionadas mediante la **OrderNumber** columna.  
  
```  
SHAPE {  
    OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber  
    FROM vAssocSeqOrders ORDER BY OrderNumber')  
} APPEND (  
    {OPENQUERY([Adventure Works DW Multidimensional 2012],'SELECT OrderNumber, model FROM   
    dbo.vAssocSeqLineItems ORDER BY OrderNumber, Model')}  
  RELATE OrderNumber to OrderNumber)   
```  
  
## <a name="see-also"></a>Vea también  
 [&#60;consulta de origen de datos&#62;](../dmx/source-data-query.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de definición de datos](../dmx/dmx-statements-data-definition.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
