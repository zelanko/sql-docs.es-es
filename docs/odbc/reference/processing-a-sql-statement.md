---
title: Procesamiento de una instrucción SQL ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349a62034d598c1bfb44b891b91359d5ff184b7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280525"
---
# <a name="processing-a-sql-statement"></a>Procesar una instrucción SQL
Antes de discutir las técnicas para usar SQL mediante programación, es necesario discutir cómo se procesa una instrucción SQL. Los pasos involucrados son comunes a las tres técnicas, aunque cada técnica los realiza en diferentes momentos. En la ilustración siguiente se muestran los pasos implicados en el procesamiento de una instrucción SQL, que se describen en el resto de esta sección.  
  
 ![Pasos para procesar una instrucción SQL](../../odbc/reference/media/pr01.gif "pr01")  
  
 Para procesar una instrucción SQL, un DBMS realiza los cinco pasos siguientes:  
  
1.  El DBMS analiza primero la instrucción SQL. Divide la instrucción en palabras individuales, denominadas tokens, se asegura de que la instrucción tenga un verbo válido y cláusulas válidas, etc. Los errores de sintaxis y las faltas de ortografía se pueden detectar en este paso.  
  
2.  El DBMS valida la instrucción. Comprueba la instrucción con el catálogo del sistema. ¿Existen todas las tablas nombradas en la instrucción en la base de datos? ¿Existen todas las columnas y los nombres de columna son inequívocos? ¿Tiene el usuario los privilegios necesarios para ejecutar la instrucción? Ciertos errores semánticos se pueden detectar en este paso.  
  
3.  El DBMS genera un plan de acceso para la instrucción. El plan de acceso es una representación binaria de los pasos necesarios para llevar a cabo la instrucción; es el equivalente DBMS del código ejecutable.  
  
4.  El DBMS optimiza el plan de acceso. Explora varias formas de llevar a cabo el plan de acceso. ¿Se puede utilizar un índice para acelerar una búsqueda? ¿Debe el DBMS aplicar primero una condición de búsqueda a la tabla A y, a continuación, unirla a la tabla B, o debe comenzar con la combinación y utilizar la condición de búsqueda después? ¿Se puede evitar o reducir una búsqueda secuencial a través de una tabla a un subconjunto de la tabla? Después de explorar las alternativas, el DBMS elige una de ellas.  
  
5.  El DBMS ejecuta la instrucción ejecutando el plan de acceso.  
  
 Los pasos utilizados para procesar una instrucción SQL varían en la cantidad de acceso a la base de datos que requieren y la cantidad de tiempo que tardan. El análisis de una instrucción SQL no requiere acceso a la base de datos y se puede realizar muy rápidamente. La optimización, por otro lado, es un proceso muy intensivo en CPU y requiere acceso al catálogo del sistema. Para una consulta compleja y multitabla, el optimizador puede explorar miles de formas diferentes de llevar a cabo la misma consulta. Sin embargo, el costo de ejecutar la consulta de forma ineficiente suele ser tan alto que el tiempo invertido en la optimización es más que recuperado en una mayor velocidad de ejecución de la consulta. Esto es aún más significativo si se puede usar el mismo plan de acceso optimizado una y otra vez para realizar consultas repetitivas.
