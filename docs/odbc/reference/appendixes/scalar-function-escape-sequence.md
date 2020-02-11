---
title: Secuencia de escape de función escalar | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057068"
---
# <a name="scalar-function-escape-sequence"></a>Secuencia de Escape de la función escalar
ODBC utiliza secuencias de escape para las funciones escalares. La sintaxis de esta secuencia de escape es la siguiente:  
  
```  
{fn scalar-function}  
```  
  
## <a name="remarks"></a>Observaciones  
 En la notación BNF, la sintaxis es la siguiente:  
  
 *ODBC-Scalar-function-escape* :: =  
  
 *ODBC-ESC-Initiator* FN *función escalar ODBC-ESC-terminador*  
  
 *función escalar* :: = *nombre de función* (*lista de argumentos*)  
  
 (Las definiciones para el *nombre de función* y el nombre de *función* (lista de*argumentos*) no terminales se derivan de la lista de funciones escalares en el [Apéndice E: funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md)).  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-Terminator* :: =}  
  
 Para determinar si el origen de datos admite procedimientos y el controlador admite la sintaxis de invocación de procedimiento ODBC, una aplicación puede llamar a **SQLGetInfo**. Para obtener más información, vea el [Apéndice E: funciones escalares](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md).
