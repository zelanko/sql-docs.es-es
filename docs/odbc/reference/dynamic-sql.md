---
title: "SQL dinámico | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4c24d1dbab68a1e47b5dfe7b48dc3df86fb9f692
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="dynamic-sql"></a>SQL dinámico
Aunque SQL estático funciona bien en muchas situaciones, hay una clase de aplicaciones en el que el acceso a datos no se puede determinar de antemano. Por ejemplo, suponga que una hoja de cálculo permite al usuario especificar una consulta, que la hoja de cálculo, a continuación, se envía al DBMS para recuperar los datos. El contenido de esta consulta obviamente no puede conocerse al programador cuando se escribe el programa de hoja de cálculo.  
  
 Para solucionar este problema, la hoja de cálculo utiliza una forma de SQL incrustado denominado SQL dinámico. A diferencia de las instrucciones SQL estáticas, que están codificados de forma rígida en el programa, instrucciones SQL dinámicas se pueden generar en tiempo de ejecución y coloca en una variable de host de la cadena. A continuación, se envían del DBMS para su procesamiento. Debido a que el DBMS debe generar un plan de acceso en tiempo de ejecución de instrucciones SQL dinámicas, SQL dinámico es generalmente más lento que SQL estático. Cuando se compila un programa que contiene instrucciones SQL dinámicas, las instrucciones SQL dinámicas no se eliminan desde el programa, como en SQL estático. En su lugar, se reemplazan por una llamada de función que pasa la instrucción para el sistema DBMS; instrucciones SQL estáticas en el mismo programa se tratan normalmente.  
  
 Es la manera más sencilla de ejecutar una instrucción SQL dinámica con una instrucción EXECUTE IMMEDIATE. Esta instrucción pasa la instrucción SQL en el DBMS de compilación y ejecución.  
  
 Una desventaja de la instrucción EXECUTE IMMEDIATE es que el DBMS deben pasar por cada uno de los cinco pasos de procesamiento de una instrucción SQL cada vez que se ejecuta la instrucción. La sobrecarga implicada en este proceso puede ser significativa si muchas instrucciones se ejecutan de forma dinámica y resulta desperdician si estas instrucciones son similares. Para solucionar esta situación, SQL dinámico ofrece una forma optimizada de ejecución llamada a la ejecución preparada, lo cual utiliza los siguientes pasos:  
  
1.  El programa crea una instrucción SQL en un búfer, igual que para la instrucción EXECUTE IMMEDIATE. En lugar de variables de host, un signo de interrogación (?) se pueden sustituir por una constante en cualquier lugar en el texto de la instrucción para indicar que un valor de la constante se proporcionarán más adelante. Se llama el signo de interrogación como marcador de parámetro.  
  
2.  El programa pasa la instrucción SQL al DBMS con una instrucción PREPARE, qué solicitudes que el DBMS analizar, validar y optimizar la instrucción y generar una ejecución plan para él. A continuación, el programa utiliza una instrucción EXECUTE (no una instrucción EXECUTE IMMEDIATE) para ejecutar la instrucción preparada en un momento posterior. Pasa los valores de parámetro de la instrucción a través de una estructura de datos especial denominada el área de datos de SQL o SQLDA.  
  
3.  El programa puede usar la instrucción EXECUTE repetidamente, proporcionar valores de parámetro diferente cada vez que se ejecuta la instrucción dinámica.  
  
 Ejecución preparada todavía no es igual que SQL estático. En SQL estático, los cuatro primeros pasos de procesamiento de una instrucción SQL tienen lugar en tiempo de compilación. En una ejecución preparada, estos pasos siguen realizando en tiempo de ejecución, pero se realizan una sola vez; ejecución del plan tiene lugar cuando se llama a EXECUTE. Esto ayuda a eliminar algunas de las desventajas de rendimiento inherentes a la arquitectura de SQL dinámico. La ilustración siguiente muestra las diferencias entre SQL estáticos, SQL dinámico con la ejecución inmediata y SQL dinámico con la ejecución preparada.
