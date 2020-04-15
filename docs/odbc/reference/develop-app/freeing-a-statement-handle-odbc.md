---
title: Liberación de un control de instrucción ODBC ( Freeing a Statement Handle ODBC ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01e4cb46edf1b1a0f1c6dfaa0273c1dd5b392686
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305620"
---
# <a name="freeing-a-statement-handle-odbc"></a>Liberar un identificador de instrucción ODBC
Como se mencionó anteriormente, es más eficaz reutilizar las instrucciones que quitarlas y asignar otras nuevas. Antes de ejecutar una nueva instrucción SQL en una instrucción, las aplicaciones deben asegurarse de que la configuración de la instrucción actual es adecuada. Éstos incluyen atributos de instrucción, enlaces de parámetros y enlaces de conjunto de resultados. Por lo general, los parámetros y conjuntos de resultados para la instrucción SQL antigua deben estar sin enlazar (mediante una llamada a **SQLFreeStmt** con las opciones SQL_RESET_PARAMS y SQL_UNBIND) y rebotar para la nueva instrucción SQL.  
  
 Cuando la aplicación ha terminado de usar la instrucción, llama a **SQLFreeHandle** para liberar la instrucción. Después de liberar la instrucción, es un error de programación de la aplicación para usar el identificador de la instrucción en una llamada a una función ODBC; hacerlo tiene consecuencias indefinidas, pero probablemente fatales.  
  
 Cuando **SQLFreeHandle** se llama, el controlador libera la estructura utilizada para almacenar información sobre la instrucción.  
  
 **SQLDisconnect** libera automáticamente todas las instrucciones de una conexión.
