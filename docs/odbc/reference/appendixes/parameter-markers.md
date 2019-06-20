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
manager: craigg
ms.openlocfilehash: cda6719eb46a4a05222bd54062e6cab98459d7dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63181776"
---
# <a name="parameter-markers"></a>Marcadores de parámetros
Según la especificación de SQL-92, una aplicación no puede colocar los marcadores de parámetros en las siguientes ubicaciones. Para obtener una lista más completa, vea la especificación de SQL-92.  
  
-   En un **seleccione** lista  
  
-   Como ambos *expresiones* en un *predicado de comparación*  
  
-   Como ambos operandos de un operador binario  
  
-   Como los operandos primeros y segundo de un **BETWEEN** operación  
  
-   Como el primer y el tercer operandos de un **BETWEEN** operación  
  
-   Como la expresión y el primer valor de un **IN** operación  
  
-   Como el operando de unario + o - operación  
  
-   Como el argumento de un *referencia de funciones de conjunto*  
  
 Para obtener más información acerca de los marcadores de parámetros, vea la especificación de SQL-92. Para obtener más información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).
