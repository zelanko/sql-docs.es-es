---
title: Ejemplo de SQL incrustado | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 966962bdda79a57e83a0bce06b9254267efb474c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068659"
---
# <a name="embedded-sql-example"></a>Ejemplo de SQL incrustado
El código siguiente es un sencillo programa de SQL incrustado, escrito en C. El programa muestra muchas de las técnicas de SQL incrustadas, pero no todas. El programa solicita al usuario un número de pedido, recupera el número de cliente, el vendedor y el estado del pedido, y muestra la información recuperada en la pantalla.  
  
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
  
 Tenga en cuenta lo siguiente sobre este programa:  
  
-   **Variables de host** Las variables de host se declaran en una sección entre las palabras clave **Begin DECLARE Section** y **End declare Section** . Cada nombre de variable de host tiene como prefijo un signo de dos puntos (:) Cuando aparece en una instrucción SQL incrustada. Los dos puntos permiten al precompilador distinguir entre las variables de host y los objetos de base de datos, como tablas y columnas, que tienen el mismo nombre.  
  
-   **Tipos de datos** Los tipos de datos admitidos por un DBMS y un lenguaje host pueden ser bastante diferentes. Esto afecta a las variables de host porque juegan un rol dual. Por un lado, las variables de host son variables de programa, declaradas y manipuladas por instrucciones de lenguaje de host. Por otro lado, se usan en instrucciones SQL incrustadas para recuperar datos de la base de datos. Si no hay ningún tipo de idioma de host que corresponda a un tipo de datos de DBMS, el DBMS convierte automáticamente los datos. Sin embargo, dado que cada DBMS tiene sus propias reglas e idiosincrasia asociadas al proceso de conversión, los tipos de variable de host deben elegirse con cuidado.  
  
-   **Control de errores** DBMS informa de los errores en tiempo de ejecución al programa de aplicaciones a través de un área de comunicaciones de SQL o SQLCA. En el ejemplo de código anterior, la primera instrucción SQL incrustada es incluir SQLCA. Esto indica al precompilador que incluya la estructura SQLCA en el programa. Esto es necesario siempre que el programa procese los errores devueltos por el DBMS. La... La instrucción GOTO indica al precompilador que genere código de control de errores que se bifurca en una etiqueta específica cuando se produce un error.  
  
-   **Selección de singleton** La instrucción que se usa para devolver los datos es una instrucción SELECT de singleton; es decir, solo devuelve una sola fila de datos. Por lo tanto, el ejemplo de código no declara ni utiliza cursores.
