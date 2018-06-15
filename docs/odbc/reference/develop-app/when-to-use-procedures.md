---
title: Cuándo se debe utilizar procedimientos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], about procedures
ms.assetid: 7dc9e327-dd54-4b10-9f66-9ef5c074f122
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbc53507bf2cdf3333e0d36763ad7ecf7d359155
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917380"
---
# <a name="when-to-use-procedures"></a>Cuándo se debe utilizar procedimientos
Hay una serie de ventajas de utilizar procedimientos, todos basada en el hecho de que con los procedimientos mueve instrucciones SQL desde la aplicación al origen de datos. Lo que queda en la aplicación es una llamada a procedimiento interoperable. Estas ventajas incluyen:  
  
-   **Rendimiento** procedimientos suelen ser la manera más rápida para ejecutar instrucciones SQL. Al igual que la ejecución preparada, la instrucción se compila y se ejecuta en dos pasos independientes. A diferencia de la ejecución preparada, los procedimientos se ejecutan solo en tiempo de ejecución. Se compilan en un momento diferente.  
  
-   **Las reglas de negocios** A *regla de negocios* es una regla sobre la forma en que una empresa tiene relaciones empresariales. Por ejemplo, sólo alguien con el título del vendedor podría puedan agregar nuevos pedidos de ventas. Colocar estas reglas en los procedimientos permite que las empresas individuales personalizar las aplicaciones verticales volver a escribir los procedimientos que se llama a la aplicación sin tener que modificar el código de aplicación. Por ejemplo, una aplicación de entrada de pedidos puede llamar al procedimiento **InsertOrder** con un número fijo de parámetros; exactamente cómo **InsertOrder** se implementa puede variar de una empresa a otra.  
  
-   **Replaceability** estrechamente relacionado con la colocación de las reglas de negocios en procedimientos es el hecho de que se pueden reemplazar procedimientos sin volver a compilar la aplicación. Si una regla de negocios cambia después de una empresa ha comprado e instalar una aplicación, la empresa puede cambiar el procedimiento que contiene esa regla. Desde la perspectiva de la aplicación, no ha cambiado nada; todavía llama a un procedimiento determinado para realizar una tarea determinada.  
  
-   **SQL específicos de DBMS** procedimientos proporcionan una manera para que las aplicaciones aprovechar SQL específicos de DBMS y siguen estando interoperable. Por ejemplo, un procedimiento en un DBMS que admite instrucciones de control de flujo en SQL podría interceptar y recuperarse de los errores, mientras que un procedimiento en un DBMS que no se admiten instrucciones de control de flujo puede devolver simplemente un error.  
  
-   **Procedimientos sobreviven a las transacciones** en algunos orígenes de datos, se eliminan los planes de acceso para instrucciones preparadas todas en una conexión cuando se confirma o revierte una transacción. Mediante la colocación de instrucciones SQL en procedimientos, que se almacenan permanentemente en el origen de datos, las instrucciones sobreviven a la transacción. Si los procedimientos sobreviven en preparada parcialmente preparado, o el estado cancelado es específicos del DBMS.  
  
-   **Separar desarrollo** procedimientos se pueden desarrollar por separado del resto de la aplicación. En las grandes corporaciones, esto podría proporcionar una manera más aprovechar los conocimientos de los programadores muy especializados. En otras palabras, los programadores pueden escribir código de interfaz de usuario y los programadores de la base de datos pueden escribir los procedimientos.  
  
 Generalmente se utilizan procedimientos por aplicaciones verticales y personalizadas. Estas aplicaciones tienden a realizar tareas fijas, y es posible para las llamadas a procedimiento de codificar de forma rígida en ellos. Por ejemplo, una aplicación de entrada de pedidos puede llamar a los procedimientos **InsertOrder**, **DeleteOrder**, **UpdateOrder**, y **GetOrders** .  
  
 No hay motivos para llamar a procedimientos desde aplicaciones genéricas. Normalmente se escriben procedimientos para realizar una tarea en el contexto de una determinada aplicación y por lo que no para aplicaciones genéricas. Por ejemplo, una hoja de cálculo no tiene ninguna razón para llamar a la **InsertOrder** procedimiento que se acaban de mencionar. Además, las aplicaciones genéricas no deberían construir procedimientos en tiempo de ejecución con la esperanza de proporcionar una ejecución más rápida instrucción; no solo es este probable será más lenta que la ejecución preparada o directa, también requiere instrucciones SQL específicos del DBMS.  
  
 Una excepción a esto es entornos de desarrollo de aplicaciones, que a menudo proporcionan una manera para que los programadores generar instrucciones SQL que se ejecutan los procedimientos y pueden proporcionar una manera para que los programadores de procedimientos de prueba. Este tipo de llamada entornos **SQLProcedures** a los procedimientos de lista disponibles y **SQLProcedureColumns** para obtener una lista de los parámetros de entrada, entrada/salida y salida, el procedimiento de valor devuelto y las columnas de los conjuntos de resultados creados por un procedimiento. Sin embargo, estos procedimientos deben haber sido desarrollados con antelación en cada origen de datos; Para ello se requiere instrucciones SQL específicos del DBMS.  
  
 Hay tres inconvenientes importantes al uso de procedimientos. La primera es que los procedimientos se deben escritos y compilados para cada DBMS con los que es ejecutar la aplicación. Aunque esto no es un problema para las aplicaciones personalizadas, puede aumentar considerablemente de desarrollo y tiempo de mantenimiento para las aplicaciones verticales diseñados para ejecutarse con un número de DBMS.  
  
 El segundo inconveniente es que muchos DBMS no admiten procedimientos. De nuevo, esto es más probable que sea un problema para las aplicaciones verticales diseñados para ejecutarse con un número de DBMS. Para determinar si se admiten procedimientos, llama a una aplicación **SQLGetInfo** con la opción SQL_PROCEDURES.  
  
 La desventaja terceros, que es especialmente aplicable a entornos de desarrollo de aplicaciones, es que ODBC no define ninguna gramática estándar para crear procedimientos. Es decir, aunque las aplicaciones pueden llamar a procedimientos de manera interoperacional, no pueden crearlos manera interoperacional.
