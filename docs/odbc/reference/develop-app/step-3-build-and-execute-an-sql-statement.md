---
title: 'Paso 3: Compilar y ejecutar una instrucción SQL | Documentos de Microsoft'
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
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f972fb5a0edfbbf492860e3421d5985d5e4edcc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Paso 3: Compilar y ejecutar una instrucción SQL
El tercer paso es compilar y ejecutar una instrucción SQL, como se muestra en la siguiente ilustración. Los métodos utilizados para realizar este paso están probables que varían enormemente. La aplicación puede solicitar al usuario que escriba una instrucción SQL, genere una instrucción SQL basada en la entrada de usuario, o utilizar una instrucción SQL codificadas de forma rígida. Para obtener más información, consulte [construir instrucciones SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Muestra la creación y ejecución de una instrucción SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Si la instrucción SQL contiene parámetros, la aplicación, enlaza a variables de aplicación mediante una llamada a **SQLBindParameter** para cada parámetro. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Después de la instrucción SQL se compila y se enlazan los parámetros, la instrucción se ejecuta con **SQLExecDirect**. Si la instrucción se ejecutará varias veces, puede ser preparado con **SQLPrepare** y se ejecutan con **SQLExecute**. Para obtener más información, consulte [ejecutar una instrucción](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 La aplicación podría también renunciar a ejecutar una instrucción SQL por completo y en su lugar, llame a una función para devolver un conjunto de resultados que contiene información de catálogo, como las tablas o columnas disponibles. Para obtener más información, consulte [usa de datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Acción siguiente de la aplicación depende del tipo de instrucción SQL ejecutada.  
  
|Tipo de instrucción SQL|Vaya al|  
|---------------------------|----------------|  
|**Seleccione** o función de catálogo|[El paso 4a: capturar los resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**ACTUALIZACIÓN**, **eliminar**, o **insertar**|[Paso 4b: capturar el recuento de filas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas las demás instrucciones SQL|Paso 3: Compilar y ejecutar una instrucción SQL (en este tema) o [paso 5: confirmar la transacción](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
