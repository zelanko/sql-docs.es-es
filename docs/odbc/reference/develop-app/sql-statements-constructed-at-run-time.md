---
title: Instrucciones SQL construidas en tiempo de ejecución | Microsoft Docs
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
ms.openlocfilehash: 8333000c9bb806116244ac6d4f654fa195205868
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107462"
---
# <a name="sql-statements-constructed-at-run-time"></a>Instrucciones SQL creadas en tiempo de ejecución
Las aplicaciones que realizan el análisis ad hoc suelen compilar instrucciones SQL en tiempo de ejecución. Por ejemplo, una hoja de cálculo podría permitir a un usuario seleccionar columnas de las que recuperar datos:  
  
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
  
 Otra clase de aplicaciones que normalmente construye instrucciones SQL en tiempo de ejecución son los entornos de desarrollo de aplicaciones. Sin embargo, las instrucciones que generan están codificadas de forma rígida en la aplicación que están compilando, donde normalmente se pueden optimizar y probar.  
  
 Las aplicaciones que crean instrucciones SQL en tiempo de ejecución pueden proporcionar una gran flexibilidad al usuario. Como se puede ver en el ejemplo anterior, que no admitía las operaciones comunes como cláusulas **Where** , cláusulas **order by** o combinaciones, la creación de instrucciones SQL en tiempo de ejecución es enormemente más compleja que las instrucciones de codificación rígida. Además, la prueba de estas aplicaciones es problemática porque puede construir un número arbitrario de instrucciones SQL.  
  
 Una posible desventaja de la construcción de instrucciones SQL en tiempo de ejecución es que tarda mucho más tiempo en construir una instrucción que usar una instrucción codificada de forma rígida. Afortunadamente, esto rara vez es un problema. Estas aplicaciones suelen ser de uso intensivo de la interfaz de usuario y el tiempo que la aplicación invierte en construir instrucciones SQL suele ser pequeño en comparación con el tiempo que el usuario invierte en introducir criterios.
