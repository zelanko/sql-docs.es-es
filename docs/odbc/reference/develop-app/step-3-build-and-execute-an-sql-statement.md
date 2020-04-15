---
title: 'Paso 3: Generar y ejecutar una instrucción SQL ? Microsoft Docs'
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306836"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Paso 3: Compilación y ejecución de una instrucción SQL
El tercer paso es compilar y ejecutar una instrucción SQL, como se muestra en la siguiente ilustración. Es probable que los métodos utilizados para realizar este paso varíen enormemente. La aplicación puede solicitar al usuario que escriba una instrucción SQL, cree una instrucción SQL basada en la entrada del usuario o use una instrucción SQL codificada de forma rígida. Para obtener más información, vea [Construir instrucciones SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Muestra cómo compilar y ejecutar una instrucción SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Si la instrucción SQL contiene parámetros, la aplicación los enlaza a variables de aplicación mediante una llamada a **SQLBindParameter** para cada parámetro. Para obtener más información, consulte [Parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Después de compilar la instrucción SQL y enlazar los parámetros, la instrucción se ejecuta con **SQLExecDirect**. Si la instrucción se ejecutará varias veces, se puede preparar con **SQLPrepare** y ejecutarse con **SQLExecute**. Para obtener más información, consulte [Ejecución de una instrucción](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 La aplicación también puede dejar de ejecutar una instrucción SQL por completo y, en su lugar, llamar a una función para devolver un conjunto de resultados que contiene información de catálogo, como las columnas o tablas disponibles. Para obtener más información, consulte [Usos de datos de catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 La siguiente acción de la aplicación depende del tipo de instrucción SQL ejecutada.  
  
|Tipo de instrucción SQL|Proceda a|  
|---------------------------|----------------|  
|**Función SELECT** o catálogo|[Paso 4a: Captura de los resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**ACTUALIZAR**, **ELIMINAR**o **INSERTAR**|[Paso 4b: Captura del recuento de filas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas las demás sentencias SQL|Paso 3: Generar y ejecutar una instrucción SQL (este tema) o [Paso 5: Confirmar la transacción](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
