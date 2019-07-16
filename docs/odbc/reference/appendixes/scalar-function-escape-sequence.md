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
ms.openlocfilehash: 36e108fcc61b2390d5fd72ac4ad322778ccfb4b2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057068"
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
  
 (Las definiciones de los elementos no terminales *nombre de la función* y *nombre de la función* (*lista de argumentos*) se derivan de la lista de funciones escalares en [ Apéndice E: Funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).)  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *ODBC-esc-terminator* ::= }  
  
 Para determinar si el origen de datos es compatible con los procedimientos y el controlador admite la sintaxis de invocación del procedimiento ODBC, una aplicación puede llamar a **SQLGetInfo**. Para obtener más información, consulte [Apéndice E: Funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
