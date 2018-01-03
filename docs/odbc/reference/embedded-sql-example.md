---
title: Incrusta ejemplo SQL | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- embedded SQL [ODBC]
ms.assetid: b8a26e05-3c82-4c5f-8f01-9de0edb645e9
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 13890248b3e724f2a41db5a3425c62dc7635b63a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="embedded-sql-example"></a>Ejemplo SQL incrustado
El código siguiente es un programa SQL incrustado simple, escrito en C. El programa muestra muchos, pero no todos, de los datos incrustados técnicas SQL. El programa solicita al usuario un número de pedido, recupera el número de cliente, el vendedor y el estado del pedido y muestra la información recuperada en la pantalla.  
  
```  
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
  
-   **Variables de host** las variables de host se declaran en una sección delimitada por la **sección declarar empezar** y **fin de declarar la sección** palabras clave. Cada nombre de variable de host viene precedida por un signo de dos puntos (:) cuando aparece en una instrucción SQL incrustada. Los dos puntos permite el precompilador distinguir entre las variables de host y objetos de base de datos, como tablas y columnas que tienen el mismo nombre.  
  
-   **Tipos de datos** los tipos de datos admitidos por un DBMS y un lenguaje host pueden ser bastante diferentes. Esto afecta a las variables de host porque desempeñan un papel doble. Por un lado, las variables de host son variables de programa, declara y manipular las instrucciones del lenguaje de host. Por otro lado, se usan en instrucciones SQL incrustadas para recuperar datos de la base de datos. Si no hay ningún tipo de lenguaje de host que corresponde a un tipo de datos DBMS, el DBMS convierte automáticamente los datos. Sin embargo, dado que cada DBMS tiene sus propias reglas e idiosincrasias asociados con el proceso de conversión, los tipos de variables de host se deben elegir con cuidado.  
  
-   **Control de errores** el DBMS informa de errores de tiempo de ejecución en el programa de las aplicaciones a través de un área de comunicaciones de SQL o SQLCA. En el ejemplo de código anterior, la primera instrucción de SQL incrustada es incluir SQLCA. Esto indica el precompilador para incluir la estructura de SQLCA en el programa. Esto es necesario cada vez que el programa procesará los errores devueltos por el DBMS. WHENEVER... GOTO (instrucción) indica el precompilador para generar el código de control de errores que realiza una bifurcación para una etiqueta específica cuando un error se produce.  
  
-   **Singleton seleccione** la instrucción utilizada para devolver los datos es una instrucción SELECT de singleton; es decir, devuelve una única fila de datos. Por lo tanto, el ejemplo de código no declara ni utilizar cursores.
