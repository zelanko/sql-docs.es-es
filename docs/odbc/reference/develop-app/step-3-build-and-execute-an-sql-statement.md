---
title: 'Paso 3: compilar y ejecutar una instrucción SQL | Microsoft Docs'
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114260"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Paso 3: Compilar y ejecutar una instrucción SQL
El tercer paso consiste en compilar y ejecutar una instrucción SQL, como se muestra en la siguiente ilustración. Es probable que los métodos utilizados para realizar este paso varíen considerablemente. Es posible que la aplicación solicite al usuario que escriba una instrucción SQL, cree una instrucción SQL basada en la entrada del usuario o use una instrucción SQL codificada de forma rígida. Para obtener más información, vea [crear instrucciones SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Muestra cómo compilar y ejecutar una instrucción SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Si la instrucción SQL contiene parámetros, la aplicación los enlaza a las variables de aplicación mediante una llamada a **SQLBindParameter** para cada parámetro. Para obtener más información, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Una vez que se compila la instrucción SQL y se enlazan los parámetros, la instrucción se ejecuta con **SQLExecDirect**. Si la instrucción se va a ejecutar varias veces, se puede preparar con **SQLPrepare** y ejecutarse con **SQLExecute**. Para obtener más información, vea [ejecutar una instrucción](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 La aplicación también puede renunciar a ejecutar una instrucción SQL y, en su lugar, llamar a una función para devolver un conjunto de resultados que contenga información de catálogo, como las columnas o tablas disponibles. Para obtener más información, vea [usos de los datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 La siguiente acción de la aplicación depende del tipo de instrucción SQL ejecutada.  
  
|Tipo de instrucción SQL|Continúe con|  
|---------------------------|----------------|  
|Función **Select** o Catalog|[El paso 4a: capturar los resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**Actualizar**, **eliminar**o **Insertar**|[Paso 4b: capturar el recuento de filas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas las demás instrucciones SQL|Paso 3: compilar y ejecutar una instrucción SQL (este tema) o [paso 5: confirmar la transacción](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
