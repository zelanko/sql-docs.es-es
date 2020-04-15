---
title: Ejemplo de SQL incrustado ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39ec504c423817c6a3e11bc954555b201b8b09c6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294176"
---
# <a name="embedded-sql-example"></a>Ejemplo de SQL incrustado
El código siguiente es un programa SQL incrustado simple, escrito en C. El programa ilustra muchas, pero no todas, de las técnicas SQL incrustadas. El programa solicita al usuario un número de pedido, recupera el número de cliente, el vendedor y el estado del pedido y muestra la información recuperada en la pantalla.  
  
```cpp  
int main() {  
   EXEC SQL INCLUDE SQLCA;  
   EXEC SQL BEGIN DECLARE SECTION;  
      int OrderID;         /* Employee ID (from user)         */  
      int CustID;            /* Retrieved customer ID         */  
      char SalesPerson[10]   /* Retrieved salesperson name      */  
      char Status[6]         /* Retrieved order status        */  
   EXEC SQL END DECLARE SECTION;  
  
   /* Set up error processing */  
   EXEC SQL WHENEVER SQLERROR GOTO query_error;  
   EXEC SQL WHENEVER NOT FOUND GOTO bad_number;  
  
   /* Prompt the user for order number */  
   printf ("Enter order number: ");  
   scanf_s("%d", &OrderID);  
  
   /* Execute the SQL query */  
   EXEC SQL SELECT CustID, SalesPerson, Status  
      FROM Orders  
      WHERE OrderID = :OrderID  
      INTO :CustID, :SalesPerson, :Status;  
  
   /* Display the results */  
   printf ("Customer number:  %d\n", CustID);  
   printf ("Salesperson: %s\n", SalesPerson);  
   printf ("Status: %s\n", Status);  
   exit();  
  
query_error:  
   printf ("SQL error: %ld\n", sqlca->sqlcode);  
   exit();  
  
bad_number:  
   printf ("Invalid order number.\n");  
   exit();  
}  
```  
  
 Tenga en cuenta lo siguiente acerca de este programa:  
  
-   **Variables de host** Las variables de host se declaran en una sección incluida por las palabras clave **BEGIN DECLARE SECTION** y END DECLARE **SECTION.** Cada nombre de variable de host tiene el prefijo de dos puntos (:) cuando aparece en una instrucción SQL incrustada. Los dos puntos permiten al precompilador distinguir entre variables de host y objetos de base de datos, como tablas y columnas, que tienen el mismo nombre.  
  
-   **Tipos de datos** Los tipos de datos admitidos por un DBMS y un lenguaje de host pueden ser muy diferentes. Esto afecta a las variables de host porque desempeñan un doble papel. Por un lado, las variables de host son variables de programa, declaradas y manipuladas por instrucciones de lenguaje host. Por otro lado, se utilizan en instrucciones SQL incrustadas para recuperar datos de base de datos. Si no hay ningún tipo de lenguaje host que corresponda a un tipo de datos DBMS, el DBMS convierte automáticamente los datos. Sin embargo, dado que cada DBMS tiene sus propias reglas e idiosincrasiaasociadas asociadas con el proceso de conversión, los tipos de variables de host deben elegirse cuidadosamente.  
  
-   **Manejo de errores** El DBMS notifica errores en tiempo de ejecución al programa de aplicaciones a través de un área de comunicaciones SQL o SQLCA. En el ejemplo de código anterior, la primera instrucción SQL incrustada es INCLUDE SQLCA. Esto indica al precompilador que incluya la estructura SQLCA en el programa. Esto es necesario siempre que el programa procesará los errores devueltos por el DBMS. El WHENEVER... La instrucción GOTO indica al precompilador que genere código de control de errores que se bifurca a una etiqueta específica cuando se produce un error.  
  
-   **Singleton SELECT** La instrucción utilizada para devolver los datos es una instrucción SELECT singleton; es decir, devuelve una sola fila de datos. Por lo tanto, el ejemplo de código no declara ni usa cursores.
