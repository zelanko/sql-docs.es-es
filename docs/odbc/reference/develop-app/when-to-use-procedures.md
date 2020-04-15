---
title: Cuándo utilizar los procedimientos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], about procedures
ms.assetid: 7dc9e327-dd54-4b10-9f66-9ef5c074f122
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31aeea226bc8c8aa41f748d1d9a97d55147c4d67
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289102"
---
# <a name="when-to-use-procedures"></a>Cuándo se debe utilizar procedimientos
El uso de procedimientos tiene varias ventajas, todo ello en función del hecho de que el uso de procedimientos mueve instrucciones SQL de la aplicación al origen de datos. Lo que queda en la aplicación es una llamada de procedimiento interoperable. Estas ventajas incluyen:  
  
-   **Rendimiento** Los procedimientos suelen ser la forma más rápida de ejecutar instrucciones SQL. Al igual que la ejecución preparada, la instrucción se compila y ejecuta en dos pasos independientes. A diferencia de la ejecución preparada, los procedimientos se ejecutan solo en tiempo de ejecución. Se compilan en un momento diferente.  
  
-   **Reglas de negocio** Una regla de *negocio* es una regla sobre la forma en que una empresa hace negocios. Por ejemplo, solo alguien con el título Persona de ventas podría poder agregar nuevos pedidos de ventas. Colocar estas reglas en procedimientos permite a las empresas individuales personalizar aplicaciones verticales reescribiendo los procedimientos a los que llama la aplicación sin tener que modificar el código de la aplicación. Por ejemplo, una aplicación de entrada de pedidos podría llamar al procedimiento **InsertOrder** con un número fijo de parámetros; exactamente cómo se implementa **InsertOrder** puede variar de una empresa a una empresa.  
  
-   **Reemplazabilidad** Muy relacionado con la colocación de reglas de negocio en los procedimientos es el hecho de que los procedimientos se pueden reemplazar sin volver a compilar la aplicación. Si una regla de negocio cambia después de que una empresa haya comprado e instalado una aplicación, la empresa puede cambiar el procedimiento que contiene esa regla. Desde el punto de vista de la aplicación, nada ha cambiado; todavía llama a un procedimiento particular para llevar a cabo una tarea en particular.  
  
-   **SQL específico de DBMS** Los procedimientos proporcionan una manera para que las aplicaciones exploten SQL específicos de DBMS y sigan siendo interoperables. Por ejemplo, un procedimiento en un DBMS que admite instrucciones de control de flujo en SQL podría capturar y recuperarse de errores, mientras que un procedimiento en un DBMS que no admite instrucciones de control de flujo podría simplemente devolver un error.  
  
-   **Los procedimientos sobreviven a las transacciones** En algunos orígenes de datos, los planes de acceso para todas las instrucciones preparadas en una conexión se eliminan cuando se confirma o revierte una transacción. Al colocar instrucciones SQL en procedimientos, que se almacenan permanentemente en el origen de datos, las instrucciones sobreviven a la transacción. Si los procedimientos sobreviven en un estado preparado, parcialmente preparado o no preparado es específico de DBMS.  
  
-   **Desarrollo separado** Los procedimientos se pueden desarrollar por separado del resto de la aplicación. En las grandes corporaciones, esto podría proporcionar una manera de explotar aún más las habilidades de los programadores altamente especializados. En otras palabras, los programadores de aplicaciones pueden escribir código de interfaz de usuario y los programadores de bases de datos pueden escribir procedimientos.  
  
 Los procedimientos generalmente son utilizados por aplicaciones verticales y personalizadas. Estas aplicaciones tienden a realizar tareas fijas y es posible codificar de forma rígida las llamadas a procedimientos en ellas. Por ejemplo, una aplicación de entrada de pedidos puede llamar a los procedimientos **InsertOrder**, **DeleteOrder**, **UpdateOrder**y **GetOrders**.  
  
 Hay pocas razones para llamar a procedimientos desde aplicaciones genéricas. Los procedimientos se escriben normalmente para realizar una tarea en el contexto de una aplicación determinada y, por lo tanto, no tienen ningún uso para las aplicaciones genéricas. Por ejemplo, una hoja de cálculo no tiene ninguna razón para llamar a la **InsertOrder** procedimiento que se acaba de mencionar. Además, las aplicaciones genéricas no deben construir procedimientos en tiempo de ejecución con la esperanza de proporcionar una ejecución de instrucciones más rápida; no sólo es probable que esto sea más lento que preparado o ejecución directa, sino que también requiere instrucciones SQL específicas de DBMS.  
  
 Una excepción a esto son los entornos de desarrollo de aplicaciones, que a menudo proporcionan una manera para que los programadores crean instrucciones SQL que ejecutan procedimientos y pueden proporcionar una manera para que los programadores prueben los procedimientos. Estos entornos llaman a **SQLProcedures** para enumerar los procedimientos disponibles y **SQLProcedureColumns** para enumerar los parámetros de entrada, entrada/salida y salida, el valor devuelto del procedimiento y las columnas de los conjuntos de resultados creados por un procedimiento. Sin embargo, estos procedimientos deben desarrollarse previamente en cada fuente de datos; Para ello, se requieren instrucciones SQL específicas de DBMS.  
  
 El uso de procedimientos tiene tres desventajas importantes. La primera es que los procedimientos deben escribirse y compilarse para cada DBMS con el que se va a ejecutar la aplicación. Aunque esto no es un problema para las aplicaciones personalizadas, puede aumentar significativamente el tiempo de desarrollo y mantenimiento de las aplicaciones verticales diseñadas para ejecutarse con varios DBMS.  
  
 La segunda desventaja es que muchos DBMS no admiten procedimientos. Una vez más, esto es más probable que sea un problema para las aplicaciones verticales diseñadas para ejecutarse con un número de DBMS. Para determinar si se admiten procedimientos, una aplicación llama a **SQLGetInfo** con la opción SQL_PROCEDURES.  
  
 La tercera desventaja, que es particularmente aplicable a los entornos de desarrollo de aplicaciones, es que ODBC no define una gramática estándar para crear procedimientos. Es decir, aunque las aplicaciones pueden llamar a procedimientos de forma interoperable, no pueden crearlos de forma interoperable.
