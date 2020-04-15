---
title: Transiciones de Estado ( State Transitions) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299698"
---
# <a name="state-transitions"></a>Transiciones de estado
ODBC define *estados* discretos para cada entorno, cada conexión y cada instrucción. Por ejemplo, el entorno tiene tres estados posibles: Sin asignar (en los que no se asigna ningún entorno), Asignado (en el que se asigna un entorno pero no se asigna ninguna conexión) y Conexión (en la que se asignan un entorno y una o más conexiones). Las conexiones tienen siete estados posibles; declaraciones tienen 13 estados posibles.  
  
 Un elemento determinado, identificado por su identificador, se mueve de un estado a otro cuando la aplicación llama a una determinada función o funciones y pasa el identificador a ese elemento. Tal movimiento se llama una *transición de estado*. Por ejemplo, la asignación de un identificador de entorno con **SQLAllocHandle** mueve el entorno de Sin asignar a Asignado y liberar ese identificador con **SQLFreeHandle** lo devuelve de Asignado a Sin asignar. ODBC define un número limitado de transiciones de estado legal, que es otra forma de decir que las funciones deben llamarse en un orden determinado.  
  
 Algunas funciones, como **SQLGetConnectAttr**, no afectan en absoluto al estado. Otras funciones afectan al estado de un único elemento. Por ejemplo, **SQLDisconnect** mueve una conexión de un estado de conexión a un estado asignado. Por último, algunas funciones afectan al estado de más de un elemento. Por ejemplo, la asignación de un identificador de conexión con **SQLAllocHandle** mueve una conexión de un un Unallocated a un Allocated estado y mueve el entorno de un Allocated to a Connection estado.  
  
 Si una aplicación llama a una función fuera de orden, la función devuelve un error de *transición*de estado . Por ejemplo, si un entorno está en un estado Connection y la aplicación llama a **SQLFreeHandle** con ese identificador de entorno, **SQLFreeHandle** devuelve SQLSTATE HY010 (error de secuencia de funciones), porque solo se puede llamar cuando el entorno está en un estado Allocated. Al definir esto como una transición de estado no válida, ODBC impide que la aplicación libere el entorno mientras hay conexiones activas.  
  
 Algunas transiciones de estado son inherentes al diseño de ODBC. Por ejemplo, no es posible asignar un identificador de conexión sin asignar primero un identificador de entorno, porque la función que asigna un identificador de conexión requiere un identificador de entorno. El Administrador de controladores y los controladores aplican otras transiciones de estado. Por ejemplo, **SQLExecute** ejecuta una instrucción preparada. Si el identificador de instrucción que se le pasa no está en un estado Preparado, **SQLExecute** devuelve SQLSTATE HY010 (error de secuencia de funciones).  
  
 Desde el punto de vista de la aplicación, las transiciones de estado suelen ser sencillas: las transiciones de estado legal tienden a ir de la mano con el flujo de una aplicación bien escrita. Las transiciones de estado son más complejas para el Administrador de controladores y los controladores porque deben realizar un seguimiento del estado del entorno, cada conexión y cada instrucción. La mayor parte de este trabajo lo realiza el Administrador de controladores; la mayor parte del trabajo que deben realizar los conductores se produce con declaraciones con resultados pendientes.  
  
 Las partes 1 y 2 de este manual ("Introducción a ODBC" y "Desarrollo de aplicaciones y controladores") tienden a no mencionar explícitamente las transiciones de estado. En su lugar, describen el orden en el que se deben llamar a las funciones. Por ejemplo, "Executing Statements" indica que se debe preparar una instrucción con **SQLPrepare** antes de que se pueda ejecutar con **SQLExecute**. Para obtener una descripción completa de los estados y las transiciones de estado, incluidas las transiciones comprobadas por el Administrador de controladores y que deben comprobar los controladores, consulte [Apéndice B: Tablas](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC .
