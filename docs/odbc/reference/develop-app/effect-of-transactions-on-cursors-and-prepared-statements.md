---
title: Efecto de las transacciones en los cursores y las instrucciones preparadas | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rolling back transactions [ODBC]
- committing transactions [ODBC]
- transactions [ODBC], rolling back
- cursors [ODBC], transaction commits or roll backs
- prepared statements [ODBC]
- transactions [ODBC], cursors
ms.assetid: 523e22a2-7b53-4c25-97c1-ef0284aec76e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b9a66541f3bfa4d51560cfa16f5ab9fc0aaa0f54
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="effect-of-transactions-on-cursors-and-prepared-statements"></a>Efecto de las transacciones en los cursores y las instrucciones preparadas
Confirmar o revertir una transacción tiene el siguiente efecto en los cursores y los planes de acceso:  
  
-   Todos los cursores se cierran y se eliminan el acceso a los planes para instrucciones preparadas en esa conexión.  
  
-   Todos los cursores se cierran y acceso a los planes para instrucciones preparadas en esa conexión permanecen intactos.  
  
-   Todos los cursores permanecen abiertos y acceso a los planes para instrucciones preparadas en esa conexión permanecen intactos.  
  
 Por ejemplo, suponga que un origen de datos comporta de la primera en esta lista, el más restrictivo de estos comportamientos. Ahora supongamos que una aplicación hace lo siguiente:  
  
1.  Establece el modo de confirmación a confirmación manual.  
  
2.  Crea un conjunto de resultados de pedidos de venta en la instrucción 1.  
  
3.  Crea un conjunto de resultados de las líneas en un pedido de venta en la instrucción 2, cuando el usuario resalta ese orden.  
  
4.  Llamadas **SQLExecute** para ejecutar una instrucción de actualización por posición que se ha preparado en la instrucción 3, cuando el usuario actualiza una línea.  
  
5.  Llamadas **SQLEndTran** para confirmar la instrucción de actualización por posición.  
  
 Como consecuencia de comportamiento del origen de datos, la llamada a **SQLEndTran** en el paso 5 hace que se cierra el cursor en las instrucciones 1 y 2 y eliminar el plan de acceso en todas las instrucciones. La aplicación debe ejecutar de nuevo los conjuntos de instrucciones 1 y 2 para volver a crear el resultado y reprepare la instrucción en instrucción 3.  
  
 En el modo de confirmación automática, funciones distintas de **SQLEndTran** confirmar las transacciones:  
  
-   **SQLExecute** o **SQLExecDirect** en el ejemplo anterior, la llamada a **SQLExecute** en el paso 4 confirma una transacción. Esto hace que el origen de datos cerrar los cursores en instrucciones 1 y 2 y eliminar el plan de acceso en todas las instrucciones de esa conexión.  
  
-   **SQLBulkOperations** o **SQLSetPos** en el ejemplo anterior, suponga que en el paso 4 llama a la aplicación **SQLSetPos** con la opción SQL_UPDATE en instrucción 2, en lugar de ejecutar un instrucción update se colocan en la instrucción 3. Esto confirma una transacción y hace que el origen de datos cerrar los cursores en instrucciones 1 y 2 y descarta todos los planes de acceso en esa conexión.  
  
-   **SQLCloseCursor** en el ejemplo anterior, imagine que cuando el usuario resalta un pedido de ventas diferentes, la aplicación llama a **SQLCloseCursor** en instrucción 2 antes de crear un resultado de las líneas para las ventas nuevo orden. La llamada a **SQLCloseCursor** confirma la **seleccione** instrucción que creó el conjunto de resultados de las líneas y hace que el origen de datos cerrar el cursor en la instrucción 1 y, a continuación, descarta todos los planes de acceso en la que conexión.  
  
 Aplicaciones, especialmente basado en pantalla en el que el usuario se desplaza por el conjunto de resultados y actualizaciones o elimine filas, deben tener cuidadas al código de este comportamiento.  
  
 Para determinar cómo se comporta un origen de datos cuando una transacción se confirma o revierte, llama a una aplicación **SQLGetInfo** con las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR.
