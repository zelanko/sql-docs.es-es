---
title: 'Paso 3: Crear y ejecutar una instrucción SQL | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: a3427057e70ee27fe1108fde71c833f0c511836b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801373"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Paso 3: Compilar y ejecutar una instrucción SQL
El tercer paso es compilar y ejecutar una instrucción SQL, como se muestra en la siguiente ilustración. Es probable que los métodos utilizados para realizar este paso variar enormemente. La aplicación podría solicitar al usuario que escriba una instrucción SQL, genere una instrucción SQL basada en la entrada de usuario, o utilizar una instrucción SQL codificadas de forma rígida. Para obtener más información, consulte [construir instrucciones SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Muestra la creación y ejecución de una instrucción SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Si la instrucción SQL contiene parámetros, la aplicación, enlaza a variables de aplicación mediante una llamada a **SQLBindParameter** para cada parámetro. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Una vez que se compila la instrucción SQL y se enlazan los parámetros, la instrucción se ejecuta con **SQLExecDirect**. Si la instrucción se ejecutará varias veces, puede prepararse con **SQLPrepare** y se ejecutan con **SQLExecute**. Para obtener más información, consulte [ejecutar una instrucción](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 La aplicación podría también renuncian a ejecutar una instrucción SQL por completo y en su lugar, llame a una función para devolver un conjunto de resultados que contiene información de catálogo, como las tablas o columnas disponibles. Para obtener más información, consulte [usa de datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Acción de la aplicación siguiente depende del tipo de instrucción SQL ejecutada.  
  
|Tipo de instrucción SQL|Vaya al|  
|---------------------------|----------------|  
|**Seleccione** o función de catálogo|[El paso 4a: capturar los resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**ACTUALIZACIÓN**, **eliminar**, o **insertar**|[Paso 4b: capturar el recuento de filas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas las demás instrucciones SQL|Paso 3: Crear y ejecutar una instrucción SQL (en este tema) o [paso 5: confirmar la transacción](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
