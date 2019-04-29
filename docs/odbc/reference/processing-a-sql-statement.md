---
title: Procesar una instrucción SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edf912bf3b8073a05dd900cd00511715020ee0c2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63045510"
---
# <a name="processing-a-sql-statement"></a>Procesar una instrucción SQL
Antes de explicar las técnicas de uso de SQL mediante programación, es necesario describir cómo se procesa una instrucción SQL. Los pasos implicados son comunes a todas las tres técnicas, aunque cada una de ellas realiza en momentos diferentes. La siguiente ilustración muestra los pasos implicados en el procesamiento de una instrucción SQL, que se describen en el resto de esta sección.  
  
 ![Pasos para procesar una instrucción SQL](../../odbc/reference/media/pr01.gif "pr01")  
  
 Para procesar una instrucción SQL, un DBMS lleva a cabo los cinco pasos siguientes:  
  
1.  En primer lugar, el DBMS analiza la instrucción SQL. La instrucción desglosa en palabras individuales, denominadas tokens, asegura que la instrucción tiene un verbo válido y cláusulas válidas y así sucesivamente. En este paso, se pueden detectar errores de ortografía y errores de sintaxis.  
  
2.  El DBMS valida la instrucción. Comprueba la instrucción en el catálogo del sistema. ¿Todas las tablas con nombre en la instrucción existen en la base de datos? ¿Existen todas las columnas y los nombres de columna no son ambiguos? ¿El usuario tiene los privilegios necesarios para ejecutar la instrucción? En este paso, se pueden detectar algunos errores semánticos.  
  
3.  El DBMS genera un plan de acceso para la instrucción. El plan de acceso es una representación binaria de los pasos necesarios para llevar a cabo la instrucción; es el equivalente DBMS de código ejecutable.  
  
4.  El DBMS optimiza el plan de acceso. Explora varias maneras de llevar a cabo el plan de acceso. ¿Puede utilizarse un índice para acelerar una búsqueda? ¿Debe DBMS primero se aplican a la tabla A una condición de búsqueda y, después, conéctela a la tabla B, o debe comenzar con la combinación y usar después la condición de búsqueda? ¿Una búsqueda secuencial a través de una tabla se puede evitar o reducir a un subconjunto de la tabla? Después de explorar las alternativas, el DBMS elige uno de ellos.  
  
5.  El DBMS ejecuta la instrucción mediante la ejecución del plan de acceso.  
  
 En la cantidad de acceso de la base de datos que necesitan y la cantidad de tiempo que se tardan varían en los pasos utilizados para procesar una instrucción SQL. Analizar una instrucción SQL no requiere acceso a la base de datos y puede hacerse muy rápidamente. La optimización, por otro lado, es una muy intensivo de CPU procesar y requiere acceso al catálogo del sistema. Para una consulta compleja, varias tablas, el optimizador puede explorar miles de distintas formas de llevar a cabo la misma consulta. Sin embargo, el costo de ejecutar la consulta de forma ineficaz suele ser tan alto que más de se ha recuperado el tiempo empleado en la optimización de velocidad de ejecución de consulta. Esto es incluso más importante si el mismo plan de acceso optimizado puede utilizarse una y otra vez para realizar consultas repetitivas.
