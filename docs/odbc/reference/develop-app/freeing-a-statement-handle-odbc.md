---
title: Liberar un identificador de instrucción ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 638cf9fb3c7af73130cf1413559b9baee2a354c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069778"
---
# <a name="freeing-a-statement-handle-odbc"></a>Liberar un identificador de instrucción ODBC
Como se mencionó anteriormente, es más eficaz volver a usar las instrucciones que to quitarlos y asignar unos nuevos. Antes de ejecutar una nueva instrucción SQL en una instrucción, las aplicaciones deben asegurarse de que la configuración actual de la instrucción adecuada. Éstos incluyen atributos de instrucción, enlaces de parámetros y enlaces de conjunto de resultados. Por lo general, deben ser independiente parámetros y conjuntos de resultados para la instrucción SQL anterior (mediante una llamada a **SQLFreeStmt** con las opciones SQL_RESET_PARAMS y SQL_UNBIND) y se vuelve a enlazar para la nueva instrucción SQL.  
  
 Cuando la aplicación ha terminado de utilizar la instrucción, llama a **SQLFreeHandle** para liberar la instrucción. Tras liberar la instrucción, es un error de programación de aplicaciones para usar el identificador de la instrucción en una llamada a una función ODBC; Si lo hace por lo que tiene consecuencias indefinidas, pero probablemente irrecuperables.  
  
 Cuando **SQLFreeHandle** se llama, las versiones de controlador utiliza la estructura para almacenar información acerca de la instrucción.  
  
 **SQLDisconnect** libera automáticamente todas las instrucciones de una conexión.
