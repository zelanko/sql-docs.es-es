---
title: Instrucciones SQL construidas en tiempo de ejecución Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 795335be2a2a3aab1be6dac26bf6d213161fe42e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301976"
---
# <a name="sql-statements-constructed-at-run-time"></a>Instrucciones SQL creadas en tiempo de ejecución
Las aplicaciones que realizan análisis ad hoc suelen generar instrucciones SQL en tiempo de ejecución. Por ejemplo, una hoja de cálculo puede permitir a un usuario seleccionar columnas de las que recuperar datos:  
  
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
  
 Otra clase de aplicaciones que normalmente construye instrucciones SQL en tiempo de ejecución son los entornos de desarrollo de aplicaciones. Sin embargo, las instrucciones que construyen están codificadas de forma rígida en la aplicación que están creando, donde normalmente se pueden optimizar y probar.  
  
 Las aplicaciones que construyen instrucciones SQL en tiempo de ejecución pueden proporcionar una gran flexibilidad al usuario. Como se puede ver en el ejemplo anterior, que ni siquiera admitía operaciones comunes como cláusulas **WHERE,** cláusulas **ORDER BY** o combinaciones, la construcción de instrucciones SQL en tiempo de ejecución es mucho más compleja que las instrucciones de codificación rígida. Además, probar estas aplicaciones es problemático porque pueden construir un número arbitrario de instrucciones SQL.  
  
 Una desventaja potencial de construir instrucciones SQL en tiempo de ejecución es que se necesita mucho más tiempo para construir una instrucción que usar una instrucción codificada de forma rígida. Afortunadamente, esto rara vez es una preocupación. Estas aplicaciones tienden a ser intensivas en interfaz de usuario, y el tiempo que la aplicación pasa construyendo instrucciones SQL es generalmente pequeño en comparación con el tiempo que el usuario pasa introduciendo criterios.
