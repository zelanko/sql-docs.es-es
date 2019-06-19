---
title: Cuándo se debe utilizar procedimientos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 82e71e6849902eb2f02423560c534056112a139a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208384"
---
# <a name="when-to-use-procedures"></a>Cuándo se debe utilizar procedimientos
Hay una serie de ventajas de utilizar los procedimientos, todos basada en el hecho de que el uso de procedimientos mueve las instrucciones SQL desde la aplicación en el origen de datos. Lo que queda en la aplicación es una llamada a procedimiento interoperable. Estas ventajas incluyen:  
  
-   **Rendimiento** procedimientos suelen ser la manera más rápida para ejecutar instrucciones SQL. Al igual que la ejecución preparada, la instrucción se compila y ejecuta en dos pasos independientes. A diferencia de la ejecución preparada, los procedimientos se ejecutan solo en tiempo de ejecución. Se compilan en un momento diferente.  
  
-   **Las reglas de negocios** A *regla de negocios* es una regla sobre la manera en que una empresa tiene relaciones empresariales. Por ejemplo, solo un usuario con el título del encargado de ventas que se le permita agregar nuevos pedidos de ventas. Colocación de estas reglas en los procedimientos permite a las empresas individuales personalizar aplicaciones verticales al volver a escribir los procedimientos llamados por la aplicación sin tener que modificar el código de aplicación. Por ejemplo, una aplicación de entrada de pedidos podría llamar al procedimiento **InsertOrder** con un número fijo de parámetros; exactamente cómo **InsertOrder** se implementa puede variar de una empresa a otra.  
  
-   **Replaceability** estrechamente relacionada con la colocación de las reglas de negocios en procedimientos es el hecho de que se pueden reemplazar procedimientos sin volver a compilar la aplicación. Si una regla de negocios cambia después de una empresa ha comprado e instalar una aplicación, la empresa puede cambiar el procedimiento que contiene esa regla. Desde la perspectiva de la aplicación, ha cambiado nada; todavía se llama un procedimiento específico para realizar una tarea determinada.  
  
-   **SQL específicos para DBMS** procedimientos proporcionan una manera para que las aplicaciones aprovechar SQL específicos de DBMS y siguen estando interoperable. Por ejemplo, un procedimiento en un sistema DBMS que admite instrucciones de control de flujo en SQL podría interceptar y recuperarse de errores, mientras que un procedimiento en un DBMS que no es compatible con las instrucciones de control de flujo simplemente podría devolver un error.  
  
-   **Procedimientos sobreviven a las transacciones** en algunos orígenes de datos, se eliminan los planes de acceso para instrucciones preparadas todo en una conexión cuando se confirma o revierte una transacción. Mediante la colocación de instrucciones SQL en procedimientos, que se almacenan permanentemente en el origen de datos, las instrucciones sobreviven a la transacción. Si sobreviven los procedimientos en preparada parcialmente preparado, o el estado cancelado es específicos para DBMS.  
  
-   **Separar desarrollo** se pueden desarrollar procedimientos por separado del resto de la aplicación. En las grandes corporaciones, esto podría proporcionar una manera de aprovechar aún más los conocimientos de los programadores muy especializados. En otras palabras, los programadores de aplicaciones pueden escribir código de interfaz de usuario y los programadores de base de datos pueden escribir los procedimientos.  
  
 Los procedimientos se suelen usar las aplicaciones personalizadas y vertical. Estas aplicaciones tienden a realizar tareas fijas, y es posible a las llamadas de procedimiento de codificar de forma rígida en ellos. Por ejemplo, una aplicación de entrada de pedidos podría llamar a los procedimientos **InsertOrder**, **DeleteOrder**, **UpdateOrder**, y **GetOrders** .  
  
 Hay pocas razones para llamar a procedimientos desde aplicaciones genéricas. Normalmente se escriben los procedimientos para realizar una tarea en el contexto de una determinada aplicación y así no tener ningún uso para aplicaciones genéricas. Por ejemplo, una hoja de cálculo no tiene ninguna razón para llamar a la **InsertOrder** procedimiento acabo de mencionar. Además, las aplicaciones genéricas no deben construir los procedimientos en tiempo de ejecución con la esperanza de que proporciona una ejecución más rápida instrucción; no sólo es probable que sea más lenta que la ejecución preparada o directa, este también requiere instrucciones SQL específicos para DBMS.  
  
 Una excepción a esto es que los entornos de desarrollo de aplicaciones que suelen ofrecen un método para los programadores crear instrucciones SQL que se ejecutan los procedimientos y pueden proporcionar una manera para los programadores de procedimientos de prueba. Dicha llamada entornos **SQLProcedures** a los procedimientos disponibles de lista y **SQLProcedureColumns** para enumerar los parámetros de entrada, entrada/salida y salida, el procedimiento de valor devuelto y las columnas de los conjuntos de resultados creados por un procedimiento. Sin embargo, dichos procedimientos deben desarrollarse con antelación en cada origen de datos; Para ello se requiere instrucciones SQL específicos para DBMS.  
  
 Hay tres desventajas principales del uso de procedimientos. La primera es que los procedimientos es necesario escritos y compilar para cada DBMS con los que es ejecutar la aplicación. Aunque esto no es un problema para las aplicaciones personalizadas, puede aumentar considerablemente de desarrollo y tiempo de mantenimiento para aplicaciones verticales diseñado para ejecutarse con un número de DBMS.  
  
 La segunda desventaja es que muchos DBMS no admiten procedimientos. Nuevamente, esto es más probable que sea un problema para las aplicaciones verticales diseñado para ejecutarse con un número de DBMS. Para determinar si se admiten los procedimientos, una aplicación llama a **SQLGetInfo** con la opción SQL_PROCEDURES.  
  
 La desventaja terceros, que es especialmente aplicable a entornos de desarrollo de aplicaciones, es que ODBC no define ninguna gramática estándar para la creación de procedimientos. Es decir, aunque las aplicaciones pueden llamar procedimientos manera interoperacional, no pueden crearlos manera interoperacional.
