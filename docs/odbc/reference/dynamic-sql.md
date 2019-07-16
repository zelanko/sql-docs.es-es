---
title: SQL dinámico | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 131abdd4a401e336ccd78ca79fdf6666b1911fee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915456"
---
# <a name="dynamic-sql"></a>SQL dinámico
Aunque SQL estático funciona bien en muchas situaciones, hay una clase de aplicaciones en la que el acceso a datos no se puede determinar de antemano. Por ejemplo, suponga que una hoja de cálculo permite que un usuario que escriba una consulta, que la hoja de cálculo, a continuación, envía a la instancia de DBMS para recuperar los datos. El contenido de esta consulta obviamente no puede conocerse al programador cuando se escribe el programa de hoja de cálculo.  
  
 Para solucionar este problema, la hoja de cálculo utiliza un formulario de SQL incrustado denominado SQL dinámico. A diferencia de las instrucciones SQL estáticas, que están codificados en el sistema, instrucciones SQL dinámicas se pueden desarrollar en tiempo de ejecución y coloca en una variable de host de la cadena. A continuación, se envían a DBMS para su procesamiento. Dado que el DBMS debe generar un plan de acceso en tiempo de ejecución de instrucciones SQL dinámicas, SQL dinámico es normalmente más lento que SQL estático. Cuando se compila un programa que contiene instrucciones SQL dinámicas, las instrucciones SQL dinámicas no se quitan del programa, como en SQL estático. En su lugar, se reemplazan por una llamada de función que se pasa la instrucción a DBMS; instrucciones SQL estáticas en el mismo programa se tratan con normalidad.  
  
 Es la manera más sencilla de ejecutar una instrucción SQL dinámica con una instrucción EXECUTE IMMEDIATE. Esta instrucción pasa la instrucción SQL a la instancia de DBMS para la compilación y ejecución.  
  
 Una desventaja de la instrucción EXECUTE IMMEDIATE es que el DBMS debe pasar por cada uno de los cinco pasos de procesamiento de una instrucción SQL cada vez que se ejecuta la instrucción. La sobrecarga implicada en este proceso puede ser significativa si muchas de las instrucciones se ejecutan de forma dinámica, y es un desperdicio si esas instrucciones son similares. Para solucionar esta situación, SQL dinámico ofrece una forma optimizada de ejecución llama a la ejecución preparada, que utiliza los siguientes pasos:  
  
1.  El programa construye una instrucción SQL en un búfer, al igual que para la instrucción EXECUTE IMMEDIATE. En lugar de variables de host, se puede sustituir un signo de interrogación (?) para una constante en cualquier lugar en el texto de la instrucción para indicar que se proporcionarán un valor para la constante más adelante. Se llama el signo de interrogación como marcador de parámetro.  
  
2.  El programa pasa a la instrucción SQL para la instancia de DBMS con una instrucción PREPARE, que solicita que el DBMS analizar, validar y optimizar la instrucción y generar una ejecución de plan para él. El programa, a continuación, usa una instrucción EXECUTE (no una instrucción EXECUTE IMMEDIATE) para ejecutar la instrucción preparada en un momento posterior. Pasa los valores de parámetro para la instrucción a través de una estructura de datos especial denominada SQLDA o área de datos de SQL.  
  
3.  El programa puede usar la instrucción EXECUTE repetidamente, proporcionando los valores de parámetro diferente cada vez que se ejecuta la instrucción dinámica.  
  
 Ejecución preparada todavía no es igual a SQL estático. En SQL estático, los cuatro primeros pasos de procesamiento de una instrucción SQL tienen lugar en tiempo de compilación. En la ejecución preparada, estos pasos se siguen realizando en tiempo de ejecución, pero se llevan a cabo una sola vez; ejecución del plan realiza solo cuando se llama a EXECUTE. Esto ayuda a eliminar algunos de los inconvenientes de rendimiento inherentes de la arquitectura de SQL dinámico. La ilustración siguiente muestra las diferencias entre SQL estático, SQL dinámico con la ejecución inmediata y SQL dinámico con la ejecución preparada.
