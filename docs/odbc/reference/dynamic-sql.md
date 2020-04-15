---
title: SQL dinámico ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], dynamic SQL
- SQL statements [ODBC], embedded SQL
- dynamic SQL [ODBC]
- SQL [ODBC], dynamic SQL
- embedded SQL [ODBC]
ms.assetid: 0bfb9ab7-9c15-4433-93bc-bad8b6c9d287
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56419723540114f122be2582f0de7c7e7d0c54f3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306693"
---
# <a name="dynamic-sql"></a>SQL dinámico
Aunque SQL estático funciona bien en muchas situaciones, hay una clase de aplicaciones en la que el acceso a datos no se puede determinar de antemano. Por ejemplo, supongamos que una hoja de cálculo permite a un usuario escribir una consulta, que la hoja de cálculo envía al DBMS para recuperar datos. El contenido de esta consulta obviamente no puede ser conocido por el programador cuando se escribe el programa de hoja de cálculo.  
  
 Para resolver este problema, la hoja de cálculo utiliza una forma de SQL incrustado denominado SQL dinámico. A diferencia de las instrucciones SQL estáticas, que están codificadas de forma rígida en el programa, las instrucciones SQL dinámicas se pueden generar en tiempo de ejecución y colocarse en una variable de host de cadena. A continuación, se envían al DBMS para su procesamiento. Dado que el DBMS debe generar un plan de acceso en tiempo de ejecución para instrucciones SQL dinámicas, SQL dinámico suele ser más lento que sql estático. Cuando se compila un programa que contiene instrucciones SQL dinámicas, las instrucciones SQL dinámicas no se quitan del programa, como en SQL estático. En su lugar, se reemplazan por una llamada de función que pasa la instrucción al DBMS; las instrucciones SQL estáticas en el mismo programa se tratan normalmente.  
  
 La forma más sencilla de ejecutar una instrucción SQL dinámica es con una instrucción EXECUTE IMMEDIATE. Esta instrucción pasa la instrucción SQL al DBMS para su compilación y ejecución.  
  
 Una desventaja de la instrucción EXECUTE IMMEDIATE es que el DBMS debe pasar por cada uno de los cinco pasos de procesamiento de una instrucción SQL cada vez que se ejecuta la instrucción. La sobrecarga implicada en este proceso puede ser significativa si muchas instrucciones se ejecutan dinámicamente, y es derrochadora si esas instrucciones son similares. Para hacer frente a esta situación, SQL dinámico ofrece una forma optimizada de ejecución denominada ejecución preparada, que utiliza los pasos siguientes:  
  
1.  El programa construye una instrucción SQL en un búfer, al igual que para la instrucción EXECUTE IMMEDIATE. En lugar de variables de host, se puede sustituir un signo de interrogación (?) por una constante en cualquier parte del texto de la instrucción para indicar que se proporcionará un valor para la constante más adelante. El signo de interrogación se llama como un marcador de parámetro.  
  
2.  El programa pasa la instrucción SQL al DBMS con una instrucción PREPARE, que solicita que el DBMS analice, valide y optimice la instrucción y genere un plan de ejecución para ella. A continuación, el programa utiliza una instrucción EXECUTE (no una instrucción EXECUTE IMMEDIATE) para ejecutar la instrucción PREPARE más adelante. Pasa valores de parámetro para la instrucción a través de una estructura de datos especial denominada sql Data Area o SQLDA.  
  
3.  El programa puede utilizar la instrucción EXECUTE repetidamente, proporcionando diferentes valores de parámetro cada vez que se ejecuta la instrucción dinámica.  
  
 La ejecución preparada sigue sin ser lo mismo que SQL estático. En SQL estático, los cuatro primeros pasos de procesamiento de una instrucción SQL tienen lugar en tiempo de compilación. En la ejecución preparada, estos pasos todavía tienen lugar en tiempo de ejecución, pero se realizan solo una vez; la ejecución del plan tiene lugar solo cuando se llama a EXECUTE. Esto ayuda a eliminar algunas de las desventajas de rendimiento inherentes a la arquitectura de SQL dinámico. La siguiente ilustración muestra las diferencias entre SQL estático, SQL dinámico con ejecución inmediata y SQL dinámico con ejecución preparada.
