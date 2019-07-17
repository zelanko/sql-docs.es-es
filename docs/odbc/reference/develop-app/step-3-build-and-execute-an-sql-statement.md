---
title: 'Paso 3: Compilar y ejecutar una instrucción SQL | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f0e369b74ef629c5fd7136b9098f579b5ad2b1b4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114260"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Paso 3: Compilación y ejecución de una instrucción SQL
El tercer paso es compilar y ejecutar una instrucción SQL, como se muestra en la siguiente ilustración. Es probable que los métodos utilizados para realizar este paso variar enormemente. La aplicación podría solicitar al usuario que escriba una instrucción SQL, genere una instrucción SQL basada en la entrada de usuario, o utilizar una instrucción SQL codificadas de forma rígida. Para obtener más información, consulte [construir instrucciones SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Muestra la creación y ejecución de una instrucción SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Si la instrucción SQL contiene parámetros, la aplicación, enlaza a variables de aplicación mediante una llamada a **SQLBindParameter** para cada parámetro. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Una vez que se compila la instrucción SQL y se enlazan los parámetros, la instrucción se ejecuta con **SQLExecDirect**. Si la instrucción se ejecutará varias veces, puede prepararse con **SQLPrepare** y se ejecutan con **SQLExecute**. Para obtener más información, consulte [ejecutar una instrucción](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 La aplicación podría también renuncian a ejecutar una instrucción SQL por completo y en su lugar, llame a una función para devolver un conjunto de resultados que contiene información de catálogo, como las tablas o columnas disponibles. Para obtener más información, consulte [usa de datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Acción de la aplicación siguiente depende del tipo de instrucción SQL ejecutada.  
  
|Tipo de instrucción SQL|Vaya al|  
|---------------------------|----------------|  
|**Seleccione** o función de catálogo|[Paso 4a: Capturar los resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**ACTUALIZACIÓN**, **eliminar**, o **insertar**|[Paso 4b: Capturar el recuento de filas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas las demás instrucciones SQL|Paso 3: Compilar y ejecutar una instrucción SQL (en este tema) o [paso 5: Confirmar la transacción](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
