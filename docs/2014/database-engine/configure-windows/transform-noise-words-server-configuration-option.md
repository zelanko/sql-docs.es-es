---
title: transform noise words (opción de configuración del servidor) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text queries [SQL Server], performance
- transform noise words option
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 69bd388e-a86c-4de4-b5d5-d093424d9c57
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6b79ebeaddb028b901b7f59397c29b18c6b3dbeb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48068881"
---
# <a name="transform-noise-words-server-configuration-option"></a>transform noise words (opción de configuración del servidor)
  Use la `transform noise words` opción de configuración de servidor para suprimir un mensaje de error si palabras irrelevantes, que es [las palabras irrelevantes](../../relational-databases/search/full-text-search.md), hacen que una operación booleana en una consulta de texto completo devuelva cero filas. Esta opción es útil para las consultas de texto completo que utilizan el predicado CONTAINS en el que las operaciones booleanas o las operaciones NEAR incluyen palabras irrelevantes. En la siguiente tabla se describen los valores posibles.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|Las palabras irrelevantes no se transforman. Cuando una consulta de texto completo contiene palabras irrelevantes, la consulta devuelve cero filas y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produce una advertencia. Éste es el comportamiento predeterminado.<br /><br /> Tenga en cuenta que la advertencia es una advertencia de tiempo de ejecución. Por lo tanto, si no se ejecuta la cláusula de texto completo de la consulta, no se generará la advertencia. En una consulta local solo se generará una advertencia, incluso si existen varias cláusulas de consulta de texto completo. En una consulta remota, es posible que el servidor vinculado no retransmita el error; por tanto, puede que tampoco se genere la advertencia.|  
|1|Las palabras irrelevantes se transforman. Se omiten y el resto de la consulta se evalúa.<br /><br /> Si las palabras irrelevantes se especifican en un término de proximidad, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las quita. Por ejemplo, la palabra irrelevante `is` se quita de `CONTAINS(<column_name>, 'NEAR (hello,is,goodbye)')`, transformando la consulta de búsqueda en `CONTAINS(<column_name>, 'NEAR(hello,goodbye)')`. Observe que `CONTAINS(<column_name>, 'NEAR(hello,is)')` se transformaría simplemente en `CONTAINS(<column_name>, hello)` porque solo hay un término de búsqueda válido.|  
  
## <a name="effects-of-the-transform-noise-words-setting"></a>Efectos de la opción Transformar palabras irrelevantes  
 En esta sección se muestra el comportamiento de las consultas que contienen una palabra irrelevante, "`the`", en la configuración alternativa de `transform noise words`.  Se supone que las cadenas de consulta de texto completo de ejemplo se ejecutan en una fila de tabla que contiene los datos siguientes: `[1, "The black cat"]`.  
  
> [!NOTE]  
>  Todos esos escenarios pueden generar una advertencia por palabras irrelevantes.  
  
-   Con Transformar palabras irrelevantes establecido en 0:  
  
    |Cadena de consulta|Resultado|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Sin resultados (el comportamiento es el mismo para "`the`" AND "`cat`").|  
    |"`cat`" NEAR "`the`"|Sin resultados (el comportamiento es el mismo para "`the`" NEAR "`cat`").|  
    |"`the`" AND NOT "`black`"|No hay resultados|  
    |"`black`" AND NOT "`the`"|No hay resultados|  
  
-   Con Transformar palabras irrelevantes establecido en 1:  
  
    |Cadena de consulta|Resultado|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Acierto para la fila con identificador 1|  
    |"`cat`" NEAR "`the`"|Acierto para la fila con identificador 1|  
    |"`the`" AND NOT "`black`"|No hay resultados|  
    |"`black`" AND NOT "`the`"|Acierto para la fila con identificador 1|  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se establece `transform noise words` en `1`.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'transform noise words', 1;  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
