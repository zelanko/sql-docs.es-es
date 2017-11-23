---
title: "Secuencia de Escape de la función escalar | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ca49a0f372ef192336318fc2af3135adf4c37d1e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="scalar-function-escape-sequence"></a>Secuencia de Escape de la función escalar
ODBC utiliza secuencias de escape para funciones escalares. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es la siguiente:  
  
 *ODBC escalar función escape* :: =  
  
 *Iniciador de esc de ODBC* fn *función escalar del terminador de esc de ODBC*  
  
 *función escalar* :: = *nombre de la función* (*lista de argumentos*)  
  
 (Las definiciones de los elementos no terminales *nombre de la función* y *nombre de la función* (*lista de argumentos*) se derivan de la lista de funciones escalares en [ Apéndice E: funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *Terminador de esc de ODBC* :: =}  
  
 Para determinar si el origen de datos es compatible con los procedimientos y el controlador es compatible con la sintaxis de invocación de procedimiento ODBC, una aplicación puede llamar a **SQLGetInfo**. Para obtener más información, consulte [Apéndice E: funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
