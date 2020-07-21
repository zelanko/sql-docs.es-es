---
title: Efecto de las transacciones en cursores y instrucciones preparadas | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef3cb4095410b8ccb03b0a138f65b8df2cfb1a4b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300475"
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Efecto de las transacciones en los cursores y las instrucciones preparadas
La confirmación o reversión de una transacción tiene el siguiente efecto en los cursores y los planes de acceso:  
  
-   Se cierran todos los cursores y se eliminan los planes de acceso para las instrucciones preparadas en esa conexión.  
  
-   Todos los cursores están cerrados y los planes de acceso para las instrucciones preparadas en esa conexión permanecen intactos.  
  
-   Todos los cursores permanecen abiertos y los planes de acceso para las instrucciones preparadas en esa conexión permanecen intactos.  
  
 Por ejemplo, supongamos que un origen de datos exhibe el primer comportamiento en esta lista, el más restrictivo de estos comportamientos. Ahora Supongamos que una aplicación hace lo siguiente:  
  
1.  Establece el modo de confirmación en confirmación manual.  
  
2.  Crea un conjunto de resultados de pedidos de ventas en la instrucción 1.  
  
3.  Crea un conjunto de resultados de las líneas de un pedido de ventas en la instrucción 2, cuando el usuario resalta ese pedido.  
  
4.  Llama a **SQLExecute** para ejecutar una instrucción UPDATE posicionada que se ha preparado en la instrucción 3, cuando el usuario actualiza una línea.  
  
5.  Llama a **SQLEndTran** para confirmar la instrucción UPDATE posicionada.  
  
 Debido al comportamiento del origen de datos, la llamada a **SQLEndTran** en el paso 5 hace que se cierren los cursores de las instrucciones 1 y 2 y se elimine el plan de acceso en todas las instrucciones. La aplicación debe volver a ejecutar las instrucciones 1 y 2 para volver a crear los conjuntos de resultados y volver a preparar la instrucción en la instrucción 3.  
  
 En el modo de confirmación automática, las funciones que no sean **SQLEndTran** commit Transactions:  
  
-   **SQLExecute** o **SQLExecDirect** en el ejemplo anterior, la llamada a **SQLExecute** en el paso 4 confirma una transacción. Esto hace que el origen de datos cierre los cursores en las instrucciones 1 y 2 y elimine el plan de acceso en todas las instrucciones de esa conexión.  
  
-   **SQLBulkOperations** o **SQLSetPos** en el ejemplo anterior, supongamos que en el paso 4 la aplicación llama a **SQLSetPos** con la opción SQL_UPDATE en la instrucción 2, en lugar de ejecutar una instrucción UPDATE posicionada en la instrucción 3. Esto confirma una transacción y hace que el origen de datos cierre los cursores en las instrucciones 1 y 2, y descarta todos los planes de acceso en esa conexión.  
  
-   **SQLCloseCursor** En el ejemplo anterior, supongamos que cuando el usuario resalta un pedido de venta diferente, la aplicación llama a **SQLCloseCursor** en la instrucción 2 antes de crear un resultado de las líneas para el nuevo pedido de ventas. La llamada a **SQLCloseCursor** confirma la instrucción **Select** que creó el conjunto de resultados de las líneas y hace que el origen de datos cierre el cursor en la instrucción 1 y, a continuación, descarta todos los planes de acceso en esa conexión.  
  
 Las aplicaciones, especialmente las aplicaciones basadas en pantalla en las que el usuario se desplaza por el conjunto de resultados y actualizan o eliminan filas, deben tener cuidado al codificar este comportamiento.  
  
 Para determinar el comportamiento de un origen de datos cuando se confirma o se revierte una transacción, una aplicación llama a **SQLGetInfo** con las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR.
