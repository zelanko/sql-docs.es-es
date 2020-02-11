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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.openlocfilehash: acb8d5f9687798bc0efa514ee8646b16140fcd36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100582"
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
