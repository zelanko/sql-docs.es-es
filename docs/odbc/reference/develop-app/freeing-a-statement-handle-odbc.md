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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069778"
---
# <a name="freeing-a-statement-handle-odbc"></a>Liberar un identificador de instrucción ODBC
Como se mencionó anteriormente, es más eficaz reutilizar las instrucciones que eliminarlas y asignar otras nuevas. Antes de ejecutar una nueva instrucción SQL en una instrucción, las aplicaciones deben asegurarse de que la configuración de la instrucción actual sea adecuada. Éstos incluyen atributos de instrucción, enlaces de parámetros y enlaces de conjunto de resultados. En general, los parámetros y conjuntos de resultados de la instrucción SQL anterior deben estar desenlazados (llamando a **SQLFreeStmt** con las opciones SQL_RESET_PARAMS y SQL_UNBIND) y reenlazados para la nueva instrucción SQL.  
  
 Cuando la aplicación ha terminado de usar la instrucción, llama a **SQLFreeHandle** para liberar la instrucción. Después de liberar la instrucción, se trata de un error de programación de aplicaciones para utilizar el identificador de la instrucción en una llamada a una función ODBC. Si lo hace, tendrá consecuencias indefinidas pero probablemente graves.  
  
 Cuando se llama a **SQLFreeHandle** , el controlador libera la estructura utilizada para almacenar información sobre la instrucción.  
  
 **SQLDisconnect** libera automáticamente todas las instrucciones de una conexión.
