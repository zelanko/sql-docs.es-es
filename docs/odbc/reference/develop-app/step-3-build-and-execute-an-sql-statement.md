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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8322cf5e7b4a91bfc5f5f0204cfb25fa4bdad92
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306836"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Paso 3: Compilación y ejecución de una instrucción SQL
El tercer paso consiste en compilar y ejecutar una instrucción SQL, como se muestra en la siguiente ilustración. Es probable que los métodos utilizados para realizar este paso varíen considerablemente. Es posible que la aplicación solicite al usuario que escriba una instrucción SQL, cree una instrucción SQL basada en la entrada del usuario o use una instrucción SQL codificada de forma rígida. Para obtener más información, vea [crear instrucciones SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Muestra cómo compilar y ejecutar una instrucción SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Si la instrucción SQL contiene parámetros, la aplicación los enlaza a las variables de aplicación mediante una llamada a **SQLBindParameter** para cada parámetro. Para obtener más información, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Una vez que se compila la instrucción SQL y se enlazan los parámetros, la instrucción se ejecuta con **SQLExecDirect**. Si la instrucción se va a ejecutar varias veces, se puede preparar con **SQLPrepare** y ejecutarse con **SQLExecute**. Para obtener más información, vea [ejecutar una instrucción](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 La aplicación también puede renunciar a ejecutar una instrucción SQL y, en su lugar, llamar a una función para devolver un conjunto de resultados que contenga información de catálogo, como las columnas o tablas disponibles. Para obtener más información, vea [usos de los datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 La siguiente acción de la aplicación depende del tipo de instrucción SQL ejecutada.  
  
|Tipo de instrucción SQL|Continúe con|  
|---------------------------|----------------|  
|Función **Select** o Catalog|[Paso 4a: Captura de los resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**Actualizar**, **eliminar**o **Insertar**|[Paso 4b: Captura del recuento de filas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas las demás instrucciones SQL|Paso 3: compilar y ejecutar una instrucción SQL (este tema) o [paso 5: confirmar la transacción](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
