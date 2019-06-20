---
title: Instrucciones SQL creadas en tiempo de ejecución | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- run time constructed SQL statements [ODBC]
- SQL statements [ODBC], constructing
- SQL statements [ODBC], building at run time
ms.assetid: f6554486-d49c-436a-82e3-4c158d26acd8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0573851ee93bda4aa33e8645148cf2ee66200bee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149132"
---
# <a name="sql-statements-constructed-at-run-time"></a>Instrucciones SQL creadas en tiempo de ejecución
Las aplicaciones que realizan análisis ad hoc suele generación instrucciones SQL en tiempo de ejecución. Por ejemplo, una hoja de cálculo podría permitir al usuario seleccionar las columnas de la que se va a recuperar los datos:  
  
```  
// SQL_Statements_Constructed_at_Run_Time.cpp  
#include <windows.h>  
#include <stdio.h>  
#include <sqltypes.h>  
  
int main() {  
   SQLCHAR *Statement = 0, *TableName = 0;  
   SQLCHAR **TableNamesArray, **ColumnNamesArray = 0;  
   BOOL *ColumnSelectedArray = 0;  
   BOOL  CommaNeeded;  
   SQLSMALLINT i = 0, NumColumns = 0;  
  
   // Use SQLTables to build a list of tables (TableNamesArray[]). Let the  
   // user select a table and store the selected table in TableName.  
  
   // Use SQLColumns to build a list of the columns in the selected table  
   // (ColumnNamesArray). Set NumColumns to the number of columns in the  
   // table. Let the user select one or more columns and flag these columns  
   // in ColumnSelectedArray[].  
  
   // Build a SELECT statement from the selected columns.  
   CommaNeeded = FALSE;  
   Statement = (SQLCHAR*)malloc(8);  
   strcpy_s((char*)Statement, 8, "SELECT ");  
  
   for (i = 0 ; i = NumColumns ; i++) {  
      if (ColumnSelectedArray[i]) {  
         if (CommaNeeded)  
            strcat_s((char*)Statement, sizeof(Statement), ",");  
         else  
            CommaNeeded = TRUE;  
         strcat_s((char*)Statement, sizeof(Statement), (char*)ColumnNamesArray[i]);  
      }  
   }  
  
   strcat_s((char*)Statement, 15, " FROM ");  
   // strcat_s((char*)Statement, 100, (char*)TableName);  
  
   // Execute the statement . It will be executed once, do not prepare it.  
   // SQLExecDirect(hstmt, Statement, SQL_NTS);  
}  
```  
  
 Otra clase de aplicaciones que normalmente se genera instrucciones SQL en tiempo de ejecución son entornos de desarrollo de aplicaciones. Sin embargo, las instrucciones que construyen están codificados en la aplicación que están creando, donde se pueden normalmente optimizados y probados.  
  
 Las aplicaciones que construcción instrucciones SQL en tiempo de ejecución pueden proporcionar una gran flexibilidad al usuario. Como puede observarse en el ejemplo anterior, que no admitía incluso operaciones comunes como **donde** cláusulas, **ORDER BY** cláusulas de igualdad, o combinaciones, crear instrucciones SQL en tiempo de ejecución es considerablemente más compleja que las instrucciones de forma rígida. Además, las pruebas de estas aplicaciones es problemática porque puede construir un número arbitrario de instrucciones SQL.  
  
 Una posible desventaja de crear instrucciones SQL en tiempo de ejecución es que se tarda mucho más tiempo para construir una instrucción que utilice una instrucción codificado de forma rígida. Afortunadamente, esto rara vez es una preocupación. Estas aplicaciones tienden a ser de uso intensivo de la interfaz de usuario y el tiempo que invierte la aplicación crear instrucciones SQL es generalmente pequeña en comparación con el tiempo que el usuario invierte escribiendo criterios.
