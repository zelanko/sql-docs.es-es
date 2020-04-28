---
title: Cuándo usar procedimientos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289102"
---
# <a name="when-to-use-procedures"></a>Cuándo se debe utilizar procedimientos
Hay varias ventajas en el uso de los procedimientos, todo ello en función del hecho de que el uso de procedimientos mueva instrucciones SQL de la aplicación al origen de datos. Lo que queda en la aplicación es una llamada a procedimiento interoperable. Estas ventajas incluyen:  
  
-   **Rendimiento** de Los procedimientos suelen ser la manera más rápida de ejecutar instrucciones SQL. Como la ejecución preparada, la instrucción se compila y se ejecuta en dos pasos independientes. A diferencia de la ejecución preparada, los procedimientos solo se ejecutan en tiempo de ejecución. Se compilan en un momento diferente.  
  
-   **Reglas de negocios** Una *regla de negocios* es una regla sobre la manera en que una empresa hace negocios. Por ejemplo, solo se permite que un usuario con el título sales Person agregue nuevos pedidos de venta. La colocación de estas reglas en procedimientos permite a las empresas individuales personalizar las aplicaciones verticales al volver a escribir los procedimientos a los que llama la aplicación sin tener que modificar el código de la aplicación. Por ejemplo, una aplicación de entrada de pedidos podría llamar al procedimiento **InsertOrder** con un número fijo de parámetros; exactamente cómo se implementa **InsertOrder** puede variar de una empresa a una empresa.  
  
-   **Reemplazo** En relación con la colocación de las reglas de negocios en los procedimientos, es el hecho de que los procedimientos se pueden reemplazar sin volver a compilar la aplicación. Si una regla de negocios cambia después de que una empresa haya comprado e instalado una aplicación, la empresa puede cambiar el procedimiento que contiene esa regla. Desde el punto de vista de la aplicación, no ha cambiado nada. todavía llama a un procedimiento determinado para realizar una tarea determinada.  
  
-   **SQL específico de DBMS** Los procedimientos proporcionan una manera para que las aplicaciones aprovechen SQL específico de DBMS y sigan siendo interoperables. Por ejemplo, un procedimiento en un DBMS que admita instrucciones de control de flujo en SQL podría interceptar y recuperarse de errores, mientras que un procedimiento en un DBMS que no admita instrucciones de control de flujo podría devolver simplemente un error.  
  
-   **Procedimientos que sobreviven a las transacciones** En algunos orígenes de datos, los planes de acceso para todas las instrucciones preparadas de una conexión se eliminan cuando se confirma o se revierte una transacción. Al colocar instrucciones SQL en procedimientos, que se almacenan de forma permanente en el origen de datos, las instrucciones sobreviven a la transacción. Si los procedimientos sobreviven en un estado preparado, parcialmente preparado o no preparado es específico del DBMS.  
  
-   **Desarrollo independiente** Los procedimientos se pueden desarrollar independientemente del resto de la aplicación. En grandes corporaciones, esto podría proporcionar una manera de aprovechar aún más los conocimientos de los programadores muy especializados. En otras palabras, los programadores de aplicaciones pueden escribir código de interfaz de usuario y los programadores de bases de datos pueden escribir procedimientos.  
  
 Los procedimientos se suelen usar en aplicaciones verticales y personalizadas. Estas aplicaciones tienden a realizar tareas fijas y es posible codificar las llamadas a procedimientos de forma rígida. Por ejemplo, una aplicación de entrada de pedidos podría llamar a los procedimientos **InsertOrder**, **DeleteOrder**, **UpdateOrder**y **getorders**.  
  
 Hay poca razón para llamar a los procedimientos desde aplicaciones genéricas. Los procedimientos normalmente se escriben para realizar una tarea en el contexto de una aplicación determinada y, por tanto, no pueden usarse en las aplicaciones genéricas. Por ejemplo, una hoja de cálculo no tiene ningún motivo para llamar al procedimiento **InsertOrder** que acaba de mencionar. Además, las aplicaciones genéricas no deben construir procedimientos en tiempo de ejecución con el fin de proporcionar una ejecución más rápida de la instrucción. no solo es probable que sea más lento que el preparado o la ejecución directa, sino que también requiere instrucciones SQL específicas del DBMS.  
  
 Una excepción a esto son los entornos de desarrollo de aplicaciones, que a menudo proporcionan una manera para que los programadores creen instrucciones SQL que ejecuten procedimientos y puedan proporcionar una manera para que los programadores prueben los procedimientos. Estos entornos llaman a **SQLProcedures** para enumerar los procedimientos disponibles y **SQLProcedureColumns** para enumerar los parámetros de entrada, de entrada/salida y de salida, el valor devuelto del procedimiento y las columnas de los conjuntos de resultados creados por un procedimiento. Sin embargo, estos procedimientos deben desarrollarse con antelación en cada origen de datos; Esto requiere instrucciones SQL específicas del DBMS.  
  
 Existen tres desventajas principales en el uso de procedimientos. La primera es que los procedimientos se deben escribir y compilar para cada DBMS con el que se va a ejecutar la aplicación. Aunque esto no es un problema para las aplicaciones personalizadas, puede aumentar significativamente el tiempo de desarrollo y mantenimiento de las aplicaciones verticales diseñadas para ejecutarse con varios DBMS.  
  
 La segunda desventaja es que muchos DBMS no admiten procedimientos. De nuevo, es más probable que esto sea un problema para las aplicaciones verticales diseñadas para ejecutarse con varios DBMS. Para determinar si se admiten los procedimientos, una aplicación llama a **SQLGetInfo** con la opción SQL_PROCEDURES.  
  
 El tercer inconveniente, que es especialmente aplicable a los entornos de desarrollo de aplicaciones, es que ODBC no define una gramática estándar para crear procedimientos. Es decir, aunque las aplicaciones pueden llamar a procedimientos de forma interoperacional, no pueden crearlos de forma interoperacional.
