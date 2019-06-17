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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30c1db4f850e6f181757d974ae74bb475b0cc5cc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63148989"
---
# <a name="state-transitions"></a>Transiciones de estado
ODBC define discretos *estados* para cada entorno, cada conexión y cada instrucción. Por ejemplo, el entorno tiene tres estados posibles: Sin asignar (en la que no se asigna ningún entorno), asignado (en el que se asigna a un entorno pero no se asigna a ninguna conexión) y la conexión (en el que un entorno y una o varias conexiones se asignan). Las conexiones tienen siete estados posibles; las instrucciones tener 13 estados posibles.  
  
 Un elemento determinado, según se identifica por su identificador, se mueve de un estado a otro cuando la aplicación llama a una o varias funciones determinadas y pasa el identificador a ese elemento. Se llama a este tipo de movimiento una *transición del estado*. Por ejemplo, asignar un identificador de entorno con **SQLAllocHandle** mueve el entorno de sin asignar a asignado y, liberando ese identificador con **SQLFreeHandle** devuelve asignado a Sin asignar. ODBC define un número limitado de transiciones de estado válidos, que es otra manera de decir que se deben llamar a funciones en un orden determinado.  
  
 Algunas funciones, como **SQLGetConnectAttr**, no afectan al estado en absoluto. Otras funciones afectan al estado de un único elemento. Por ejemplo, **SQLDisconnect** mueve una conexión de un estado de conexión a un estado asignado. Por último, algunas funciones afectan al estado de más de un elemento. Por ejemplo, asignar un identificador de conexión con **SQLAllocHandle** mueve una conexión de una sin asignar a un estado asignado y el entorno desde un asignado a un estado de conexión.  
  
 Si una aplicación llama a una función sin orden, la función devuelve un *error de transición de estado*. Por ejemplo, si es un entorno en un estado de conexión y la aplicación llama a **SQLFreeHandle** con ese identificador de entorno, **SQLFreeHandle** devuelve SQLSTATE HY010 (función de error de secuencia,) Dado que se puede llamar solo cuando el entorno está en un estado asignado. Al definir esto como una transición de estado no válido, ODBC impide que la aplicación libera el entorno mientras hay conexiones activas.  
  
 Algunas transiciones de estado son inherentes en el diseño de ODBC. Por ejemplo, no es posible asignar un identificador de conexión sin asignar primero un identificador de entorno, porque la función que asigna un identificador de conexión requiere un identificador de entorno. Otras transiciones de estado se aplican mediante el Administrador de controladores y los controladores. Por ejemplo, **SQLExecute** ejecuta una instrucción preparada. Si el identificador de instrucción que se pasa a no está en un estado preparado, **SQLExecute** devuelve SQLSTATE HY010 (función de error de secuencia).  
  
 Desde el punto de vista de la aplicación, las transiciones de estado son suele ser bastante sencillas: Las transiciones de estado legal tienden a van mano a mano con el flujo de una aplicación bien escrita. Las transiciones de estado son más complejas para el Administrador de controladores y los controladores porque debe realizar un seguimiento el estado del entorno, cada conexión y cada instrucción. La mayoría de este trabajo se realiza mediante el Administrador de controladores; la mayoría del trabajo que debe realizarse por los controladores se produce con las instrucciones con los resultados pendientes.  
  
 Las partes 1 y 2 de este manual ("Introducción a ODBC" y "Desarrollo de aplicaciones y controladores") tienden a no mencionar las transiciones de estado. En su lugar, se describe el orden en el que se deben llamar a funciones. Por ejemplo, "Ejecutando instrucciones" indica que una instrucción debe estar preparada con **SQLPrepare** antes de que puede ejecutarse con **SQLExecute**. Para obtener una descripción completa de los Estados y transiciones de estado, incluidos qué transiciones se comprueban mediante el Administrador de controladores y que deben comprobarse con controladores, consulte [Apéndice B: Las tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
