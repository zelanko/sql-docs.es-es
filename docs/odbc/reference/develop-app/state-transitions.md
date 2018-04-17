---
title: Transiciones de estado | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- state transitions [ODBC]
- unallocated state [ODBC]
- handles [ODBC], state transitions
- allocated state [ODBC]
- connection state [ODBC]
ms.assetid: fc741611-6535-43cc-8156-6d897d04664e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c94806fae462803c3323c3e3c5768751e53a5467
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="state-transitions"></a>Transiciones de estado
ODBC define discretos *estados* para cada entorno, cada conexión y cada instrucción. Por ejemplo, el entorno tiene tres posibles estados: sin asignar (en la que no se asigna ningún entorno), asignado (en el que se asigna un entorno pero no se asigna a ninguna conexión) y conexión (en el que un entorno y una o varias conexiones son asignado). Las conexiones tienen siete estados posibles; las instrucciones tienen 13 estados posibles.  
  
 Un elemento determinado, según se identifica por su identificador, pasa de un estado a otro cuando la aplicación llama a una función determinada o funciones y pasa el identificador a ese elemento. Se llama a este tipo movimiento una *transición del estado*. Por ejemplo, asignar un identificador de entorno con **SQLAllocHandle** mueve el entorno de sin asignar a asignado y liberar este identificador con **SQLFreeHandle** devuelve de asignado a Sin asignar. ODBC define un número limitado de las transiciones de estado válidos, que es otra manera de decir que se deben llamar a funciones en un orden determinado.  
  
 Algunas funciones, como **SQLGetConnectAttr**, no afectan el estado en absoluto. Otras funciones afectan el estado de un único elemento. Por ejemplo, **SQLDisconnect** mueve una conexión desde un estado de conexión a un estado asignado. Por último, algunas funciones afectan el estado de más de un elemento. Por ejemplo, asignar un identificador de conexión con **SQLAllocHandle** mueve una conexión de una sin asignar a un estado asignado y el entorno de un asignado a un estado de conexión.  
  
 Si una aplicación llama a una función fuera de servicio, la función devuelve un *error de transición de estado*. Por ejemplo, si un entorno está en un estado de conexión y la aplicación llama **SQLFreeHandle** con ese identificador de entorno, **SQLFreeHandle** devuelve SQLSTATE HY010 (error de secuencia de función,) porque se puede llamar solo cuando el entorno está en un estado asignado. Al definir esto como una transición de estado no válido, ODBC impide que la aplicación libera el entorno mientras hay conexiones activas.  
  
 Algunas transiciones de estado son inherentes en el diseño de ODBC. Por ejemplo, no es posible asignar un identificador de conexión sin asignar primero un identificador de entorno, porque la función que asigna un identificador de conexión requiere un identificador de entorno. Otras transiciones de estado se aplican mediante el Administrador de controladores y los controladores. Por ejemplo, **SQLExecute** ejecuta una instrucción preparada. Si el identificador de instrucción pasa a no está en un estado preparado, **SQLExecute** devuelve SQLSTATE HY010 (error de secuencia de función).  
  
 Desde el punto de vista de la aplicación, las transiciones de estado son suele ser bastante sencillas: las transiciones de estado Legal tienden a van de la mano con el flujo de una aplicación bien escrita. Las transiciones de estado son más complejas para el Administrador de controladores y los controladores porque debe realizar un seguimiento del estado del entorno, cada conexión y cada instrucción. Realiza la mayor parte de este trabajo por el Administrador de controladores; la mayoría del trabajo que se debe realizar mediante controladores se produce con las instrucciones con resultados pendientes.  
  
 Partes 1 y 2 de este manual ("Introducción a ODBC" y "Desarrollo de aplicaciones y controladores") no tienden a Mencione las transiciones de estado. En su lugar, se describe el orden en el que se deben llamar a funciones. Por ejemplo, "Ejecutando instrucciones" indica que una instrucción debe estar preparada con **SQLPrepare** antes de que se pueda ejecutar con **SQLExecute**. Para obtener una descripción completa de los Estados y transiciones de estado, como establecer qué transiciones se comprueban mediante el Administrador de controladores y que debe comprobarse controladores, consulte [tablas de transición de estado de apéndice B: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).
