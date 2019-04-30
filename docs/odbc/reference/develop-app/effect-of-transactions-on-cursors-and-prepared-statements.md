---
title: Efecto de las transacciones en los cursores y las instrucciones preparadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41c2c6b06744965144ca9d5feb27e9ea16d9903c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305716"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Efecto de las transacciones en los cursores y las instrucciones preparadas
Confirmar o revertir una transacción tiene el efecto en los cursores y los planes de acceso siguiente:  
  
-   Todos los cursores se cierran y se eliminan los planes de acceso para instrucciones preparadas en esa conexión.  
  
-   Todos los cursores se cierran y acceso a los planes para instrucciones preparadas en esa conexión permanecen intactos.  
  
-   Todos los cursores permanecen abiertos y los planes de acceso para instrucciones preparadas en esa conexión permanecen intactos.  
  
 Por ejemplo, suponga que un origen de datos comporta de la primera de esta lista, el más restrictivo de estos comportamientos. Ahora supongamos que una aplicación hace lo siguiente:  
  
1.  Establece el modo de confirmación a confirmación manual.  
  
2.  Crea un conjunto de resultados de pedidos de venta en la instrucción 1.  
  
3.  Crea un conjunto de resultados de las líneas en un pedido de ventas en la instrucción 2, cuando el usuario resalta ese orden.  
  
4.  Las llamadas **SQLExecute** para ejecutar una instrucción de actualización posicionada que se ha preparado en la instrucción 3, cuando el usuario actualiza una línea.  
  
5.  Las llamadas **SQLEndTran** para confirmar la instrucción de actualización posicionada.  
  
 Como consecuencia de comportamiento del origen de datos, la llamada a **SQLEndTran** en el paso 5 hace que para cerrar los cursores en las instrucciones 1 y 2 y eliminar el plan de acceso en todas las instrucciones. La aplicación debe ejecutar de nuevo los conjuntos de instrucciones 1 y 2 para volver a crear el resultado y reprepare la instrucción de declaración de 3.  
  
 En el modo de confirmación automática, las funciones distintas de **SQLEndTran** confirmar las transacciones:  
  
-   **SQLExecute** o **SQLExecDirect** en el ejemplo anterior, la llamada a **SQLExecute** en el paso 4 confirma una transacción. Esto hace que el origen de datos cerrar los cursores en las instrucciones 1 y 2 y eliminar el plan de acceso a todas las instrucciones de esa conexión.  
  
-   **SQLBulkOperations** o **SQLSetPos** en el ejemplo anterior, supongamos que en el paso 4 la aplicación llama a **SQLSetPos** con la opción SQL_UPDATE en instrucción 2, en lugar de ejecutar un coloca la instrucción update en la instrucción 3. Esto confirma una transacción y hace que el origen de datos cerrar los cursores en las instrucciones 1 y 2 y descarta todos los planes de acceso en esa conexión.  
  
-   **SQLCloseCursor** en el ejemplo anterior, suponga que cuando el usuario resalta otro pedido de ventas, la aplicación llama a **SQLCloseCursor** en instrucción 2 antes de crear un resultado de las líneas de las ventas nuevo orden. La llamada a **SQLCloseCursor** confirma la **seleccione** instrucción que se creó el conjunto de resultados de líneas y hace que el origen de datos cerrar el cursor en la instrucción 1 y, a continuación, se descarta todos los planes de acceso en el que conexión.  
  
 Las aplicaciones, especialmente pantalla aplicaciones basadas en el que el usuario se desplaza por el conjunto de resultados y actualizaciones o elimina las filas, deben tener cuidadas al código en torno a este comportamiento.  
  
 Para determinar cómo se comporta un origen de datos cuando se confirma o revierte una transacción, una aplicación llama a **SQLGetInfo** con las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR.
