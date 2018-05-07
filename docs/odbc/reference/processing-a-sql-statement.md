---
title: Procesar una instrucción SQL | Documentos de Microsoft
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
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7068b61081a368382b109af99f60bf6bf254e800
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="processing-a-sql-statement"></a>Procesar una instrucción SQL
Antes de hablar sobre las técnicas para usar SQL mediante programación, es necesario describir cómo se procesa una instrucción SQL. Los pasos implicados son comunes a todas las técnicas de tres, aunque cada una de ellas las realiza en momentos diferentes. En la siguiente ilustración muestra los pasos implicados en el procesamiento de una instrucción SQL, que se describen en el resto de esta sección.  
  
 ![Pasos para procesar una instrucción SQL](../../odbc/reference/media/pr01.gif "pr01")  
  
 Para procesar una instrucción SQL, un DBMS realiza los cinco pasos siguientes:  
  
1.  En primer lugar, el DBMS analiza la instrucción SQL. Divide la instrucción palabras individuales, denominadas tokens, se asegura de que la instrucción tiene un verbo válido y cláusulas válidas y así sucesivamente. En este paso, se pueden detectar errores de ortografía y errores de sintaxis.  
  
2.  El DBMS valida la instrucción. Comprueba la instrucción en el catálogo del sistema. ¿Todas las tablas con nombre en la instrucción existen en la base de datos? ¿Existen todas las columnas y los nombres de columna no son ambiguos? ¿El usuario tiene los privilegios necesarios para ejecutar la instrucción? En este paso, se pueden detectar algunos errores semánticos.  
  
3.  El DBMS genera un plan de acceso de la instrucción. El plan de acceso es una representación binaria de los pasos necesarios para llevar a cabo la instrucción; es el equivalente DBMS de código ejecutable.  
  
4.  El DBMS optimiza el plan de acceso. Explora varias maneras para llevar a cabo el plan de acceso. ¿Un índice se puede usar para acelerar una búsqueda? ¿Debe DBMS aplicar una condición de búsqueda a la tabla A y, a continuación, vuelva a unirlo a tabla B, o debe comenzar con la combinación y usar después la condición de búsqueda? ¿Puede utilizar la búsqueda secuencial a través de una tabla evitarse o reducirse a un subconjunto de la tabla? Después de analizar las alternativas, el DBMS elige una de ellas.  
  
5.  El DBMS ejecuta la instrucción mediante la ejecución del plan de acceso.  
  
 Varían en la cantidad de acceso de la base de datos que necesitan y la cantidad de tiempo que tardan en los pasos utilizados para procesar una instrucción SQL. El análisis de una instrucción SQL no requiere acceso a la base de datos y se puede realizar muy rápidamente. La optimización, por otro lado, es una CPU de muchos procesar y requiere acceso para el catálogo del sistema. Para una consulta compleja, varias tablas, el optimizador puede explorar miles de distintas formas de llevar a cabo la misma consulta. Sin embargo, el costo de ejecutar la consulta de forma ineficaz suele ser tan alto que el tiempo empleado en la optimización se recupere el más de velocidad de ejecución de consulta. Esto es incluso más importante si el mismo plan de acceso optimizado puede utilizarse una y otra vez para realizar consultas repetitivas.
