---
title: Marcadores de parámetros | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303576"
---
# <a name="parameter-markers"></a>Marcadores de parámetros
De acuerdo con la especificación SQL-92, una aplicación no puede colocar marcadores de parámetros en las siguientes ubicaciones. Para obtener una lista más completa, vea la especificación SQL-92.  
  
-   En una lista de **selección**  
  
-   Como ambas *expresiones* en un *predicado de comparación*  
  
-   Como ambos operandos de un operador binario  
  
-   Como los operandos primero y segundo de una operación **between**  
  
-   Como el primer y el tercer operando de una operación **between**  
  
-   Como la expresión y el primer valor de una operación **in**  
  
-   Como operando de una operación unaria + u  
  
-   Como argumento de una referencia a un *conjunto de funciones*  
  
 Para obtener más información sobre los marcadores de parámetros, vea la especificación SQL-92. Para obtener más información sobre los parámetros, vea parámetros de la [instrucción](../../../odbc/reference/develop-app/statement-parameters.md).
