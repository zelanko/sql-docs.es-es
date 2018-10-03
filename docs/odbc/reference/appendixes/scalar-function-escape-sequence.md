---
title: Secuencia de Escape de la función escalar | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function
- scalar functions [ODBC], escape sequences
- ODBC escape sequences [ODBC], scalar function
ms.assetid: aaf5d516-e090-445f-8839-9e39581c69c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0913458d683d7641145b262552e147033dbfc054
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47660793"
---
# <a name="scalar-function-escape-sequence"></a>Secuencia de Escape de la función escalar
ODBC utiliza secuencias de escape para funciones escalares. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es como sigue:  
  
 *Función escape ODBC-escalar* :: =  
  
 *Iniciador de esc de ODBC* fn *función escalar del terminador de esc de ODBC*  
  
 *función escalar* :: = *nombre de la función* (*lista de argumentos*)  
  
 (Las definiciones de los elementos no terminales *nombre de la función* y *nombre de la función* (*lista de argumentos*) se derivan de la lista de funciones escalares en [ Apéndice E: funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *Terminador de esc de ODBC* :: =}  
  
 Para determinar si el origen de datos es compatible con los procedimientos y el controlador admite la sintaxis de invocación del procedimiento ODBC, una aplicación puede llamar a **SQLGetInfo**. Para obtener más información, consulte [Apéndice E: funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
