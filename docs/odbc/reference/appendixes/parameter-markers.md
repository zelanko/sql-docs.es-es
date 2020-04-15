---
title: Marcadores de parámetros ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: 132473de586094f79dd34c999d44f6dd59aefaef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303576"
---
# <a name="parameter-markers"></a>Marcadores de parámetros
De acuerdo con la especificación SQL-92, una aplicación no puede colocar marcadores de parámetros en las siguientes ubicaciones. Para obtener una lista más completa, consulte la especificación SQL-92.  
  
-   En una lista **SELECT**  
  
-   Como ambas *expresiones* en un *predicado de comparación*  
  
-   Como ambos operandos de un operador binario  
  
-   Como el primer y segundo operando de una operación **BETWEEN**  
  
-   Como el primer y tercer operando de una operación **BETWEEN**  
  
-   Como la expresión y el primer valor de una operación **IN**  
  
-   Como operando de una operación unaria + o -  
  
-   Como argumento de una *referencia de función de conjunto*  
  
 Para obtener más información acerca de los marcadores de parámetro, consulte la especificación SQL-92. Para obtener más información acerca de los parámetros, vea Parámetros de [instrucción](../../../odbc/reference/develop-app/statement-parameters.md).
