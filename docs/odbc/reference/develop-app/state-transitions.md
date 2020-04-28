---
title: Transiciones de estado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3a480b7ff8953ef94f0efc4886a09731730a61b7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299698"
---
# <a name="state-transitions"></a>Transiciones de estado
ODBC define *Estados* discretos para cada entorno, cada conexión y cada instrucción. Por ejemplo, el entorno tiene tres Estados posibles: sin asignar (en el que no se asigna ningún entorno), asignado (en el que se asigna un entorno pero no se asignan conexiones) y conexión (en la que se asignan un entorno y una o varias conexiones). Las conexiones tienen siete Estados posibles: las instrucciones tienen 13 Estados posibles.  
  
 Un elemento determinado, identificado por su identificador, pasa de un estado a otro cuando la aplicación llama a una o varias funciones y pasa el identificador a ese elemento. Este movimiento se denomina *transición de estado*. Por ejemplo, la asignación de un identificador de entorno con **SQLAllocHandle** mueve el entorno de sin asignar a asignado y la liberación de ese identificador con **SQLFreeHandle** lo devuelve de asignado a sin asignar. ODBC define un número limitado de transiciones de Estado legales, que es otra manera de indicar que se debe llamar a las funciones en un orden determinado.  
  
 Algunas funciones, como **SQLGetConnectAttr**, no afectan al estado. Otras funciones afectan al estado de un solo elemento. Por ejemplo, **SQLDisconnect** mueve una conexión desde un estado de conexión a un estado asignado. Por último, algunas funciones afectan al estado de más de un elemento. Por ejemplo, la asignación de un identificador de conexión con **SQLAllocHandle** mueve una conexión desde un estado sin asignar a un estado asignado y mueve el entorno de una asignación a un estado de conexión.  
  
 Si una aplicación llama a una función fuera de orden, la función devuelve un *error de transición de estado*. Por ejemplo, si un entorno está en un estado de conexión y la aplicación llama a **SQLFreeHandle** con ese identificador de entorno, **SQLFREEHANDLE** devuelve SQLSTATE HY010 (error de secuencia de función), ya que solo se puede llamar cuando el entorno se encuentra en un estado asignado. Al definir esto como una transición de estado no válida, ODBC evita que la aplicación libere el entorno mientras haya conexiones activas.  
  
 Algunas transiciones de estado son inherentes en el diseño de ODBC. Por ejemplo, no es posible asignar un identificador de conexión sin asignar primero un identificador de entorno, porque la función que asigna un identificador de conexión requiere un identificador de entorno. El administrador de controladores y los controladores exigen otras transiciones de estado. Por ejemplo, **SQLExecute** ejecuta una instrucción preparada. Si el identificador de instrucción pasado no está en un estado preparado, **SQLExecute** devuelve SQLSTATE HY010 (error de secuencia de función).  
  
 Desde el punto de vista de la aplicación, las transiciones de Estado suelen ser sencillas: las transiciones de Estado legales tienden a estar a mano con el flujo de una aplicación bien escrita. Las transiciones de estado son más complejas para el administrador de controladores y los controladores, ya que deben realizar un seguimiento del estado del entorno, de cada conexión y de cada instrucción. La mayor parte de este trabajo se realiza mediante el administrador de controladores. la mayor parte del trabajo que deben realizar los controladores se produce con instrucciones con resultados pendientes.  
  
 Las partes 1 y 2 de este manual ("Introducción a ODBC" y "desarrollo de aplicaciones y controladores") tienden a no mencionar explícitamente las transiciones de estado. En su lugar, describen el orden en el que se debe llamar a las funciones. Por ejemplo, "ejecutar instrucciones" indica que una instrucción debe estar preparada con **SQLPrepare** para poder ejecutarse con **SQLExecute**. Para obtener una descripción completa de los Estados y las transiciones de estado, incluidas las transiciones que el administrador de controladores comprueba y las que deben comprobar los controladores, consulte [Apéndice B: tablas de transición de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
