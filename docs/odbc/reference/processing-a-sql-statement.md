---
description: Procesar una instrucción SQL
title: Procesando una instrucción SQL | Microsoft Docs
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
ms.openlocfilehash: b4ce614f6dcf4c1fe0ab1e1c806b966b4267e7fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476222"
---
# <a name="processing-a-sql-statement"></a>Procesar una instrucción SQL
Antes de analizar las técnicas de uso de SQL mediante programación, es necesario analizar cómo se procesa una instrucción SQL. Los pasos implicados son comunes a las tres técnicas, aunque cada técnica las realiza en momentos diferentes. En la ilustración siguiente se muestran los pasos necesarios para procesar una instrucción SQL, que se describen en el resto de esta sección.  
  
 ![Pasos para procesar una instrucción SQL](../../odbc/reference/media/pr01.gif "pr01")  
  
 Para procesar una instrucción SQL, un DBMS realiza los cinco pasos siguientes:  
  
1.  El DBMS analiza primero la instrucción SQL. Divide la instrucción en palabras individuales, denominadas tokens, garantiza que la instrucción tiene un verbo válido y cláusulas válidas, y así sucesivamente. En este paso se pueden detectar errores de sintaxis y errores ortográficos.  
  
2.  El DBMS valida la instrucción. Comprueba la instrucción en el catálogo del sistema. ¿Todas las tablas mencionadas en la instrucción existen en la base de datos? ¿Existen todas las columnas y los nombres de columna no son ambiguos? ¿El usuario tiene los privilegios necesarios para ejecutar la instrucción? En este paso se pueden detectar ciertos errores semánticos.  
  
3.  El DBMS genera un plan de acceso para la instrucción. El plan de acceso es una representación binaria de los pasos necesarios para llevar a cabo la instrucción; es el equivalente de DBMS del código ejecutable.  
  
4.  El DBMS optimiza el plan de acceso. Explora varias formas de llevar a cabo el plan de acceso. ¿Se puede usar un índice para acelerar una búsqueda? ¿El DBMS debe aplicar primero una condición de búsqueda a la tabla a y, a continuación, unirla a la tabla B, o debe comenzar con la combinación y usar la condición de búsqueda después? ¿Se puede evitar o reducir una búsqueda secuencial a través de una tabla a un subconjunto de la tabla? Después de explorar las alternativas, el DBMS elige una de ellas.  
  
5.  El DBMS ejecuta la instrucción ejecutando el plan de acceso.  
  
 Los pasos que se usan para procesar una instrucción SQL varían en la cantidad de acceso a la base de datos que requieren y en la cantidad de tiempo que se tardan. El análisis de una instrucción SQL no requiere acceso a la base de datos y puede realizarse muy rápidamente. La optimización, por otro lado, es un proceso muy intensivo de la CPU y requiere acceso al catálogo del sistema. Para una consulta compleja de varias tablas, el optimizador puede explorar miles de maneras diferentes de llevar a cabo la misma consulta. Sin embargo, el costo de ejecutar la consulta de forma poco eficaz suele ser tan alto que el tiempo dedicado a la optimización es mayor que el que se recupera en una mayor velocidad de ejecución de consulta. Esto es aún más importante si el mismo plan de acceso optimizado se puede usar una y otra vez para realizar consultas repetitivas.
