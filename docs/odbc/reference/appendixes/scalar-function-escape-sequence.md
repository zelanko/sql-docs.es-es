---
title: Secuencia de Escape de la función escalar | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 513df8ccd679ec2236822f780400c3cc39e37609
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
