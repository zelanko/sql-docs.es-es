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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915456"
---
# <a name="dynamic-sql"></a>SQL dinámico
Aunque SQL estático funciona bien en muchos casos, hay una clase de aplicaciones en las que el acceso a los datos no se puede determinar de antemano. Por ejemplo, supongamos que una hoja de cálculo permite al usuario escribir una consulta, que la hoja de cálculo envía a la DBMS para recuperar los datos. Obviamente, el programador no puede conocer el contenido de esta consulta cuando se escribe el programa de hojas de cálculo.  
  
 Para solucionar este problema, la hoja de cálculo usa una forma de SQL incrustado denominado SQL dinámico. A diferencia de las instrucciones SQL estáticas, que están codificadas de forma rígida en el programa, se pueden crear instrucciones SQL dinámicas en tiempo de ejecución y colocarlas en una variable de host de cadena. A continuación, se envían al DBMS para su procesamiento. Dado que el DBMS debe generar un plan de acceso en tiempo de ejecución para las instrucciones SQL dinámicas, SQL dinámico suele ser más lento que SQL estático. Cuando se compila un programa que contiene instrucciones SQL dinámicas, las instrucciones SQL dinámicas no se quitan del programa, como en SQL estático. En su lugar, se reemplazan por una llamada de función que pasa la instrucción al DBMS; las instrucciones SQL estáticas del mismo programa se tratan normalmente.  
  
 La manera más sencilla de ejecutar una instrucción SQL dinámica es con una instrucción EXECUTe Immediate. Esta instrucción pasa la instrucción SQL al DBMS para compilar y ejecutar.  
  
 Una desventaja de la instrucción EXECUTe Immediate es que el DBMS debe pasar por cada uno de los cinco pasos de procesamiento de una instrucción SQL cada vez que se ejecuta la instrucción. La sobrecarga implicada en este proceso puede ser significativa si muchas de las instrucciones se ejecutan de forma dinámica y es una pérdida de las instrucciones si son similares. Para solucionar esta situación, SQL dinámico ofrece una forma optimizada de ejecución denominada ejecución preparada, que usa los pasos siguientes:  
  
1.  El programa crea una instrucción SQL en un búfer, tal y como lo hace para la instrucción EXECUTe Immediate. En lugar de las variables de host, se puede sustituir un signo de interrogación (?) por una constante en cualquier parte del texto de la instrucción para indicar que se proporcionará un valor para la constante más adelante. Se llama al signo de interrogación como marcador de parámetro.  
  
2.  El programa pasa la instrucción SQL al DBMS con una instrucción PREPARE, que solicita que el DBMS analice, valide y optimice la instrucción y genere un plan de ejecución para ella. Después, el programa usa una instrucción EXECUTe (no una instrucción EXECUTe Immediate) para ejecutar la instrucción PREPARE en otro momento. Pasa los valores de parámetro para la instrucción a través de una estructura de datos Especial denominada área de datos SQL o SQLDA.  
  
3.  El programa puede utilizar la instrucción EXECUTe varias veces, proporcionando diferentes valores de parámetro cada vez que se ejecuta la instrucción dinámica.  
  
 La ejecución preparada todavía no es lo mismo que SQL estático. En SQL estático, los cuatro primeros pasos para procesar una instrucción SQL tienen lugar en tiempo de compilación. En la ejecución preparada, estos pasos se siguen produciendo en tiempo de ejecución, pero solo se realizan una vez. la ejecución del Plan solo tiene lugar cuando se llama a EXECUTe. Esto ayuda a eliminar algunas de las desventajas de rendimiento inherentes a la arquitectura de SQL dinámico. En la ilustración siguiente se muestran las diferencias entre SQL estático, SQL dinámico con ejecución inmediata y SQL dinámico con ejecución preparada.
