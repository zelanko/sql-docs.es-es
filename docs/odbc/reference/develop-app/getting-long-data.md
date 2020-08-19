---
description: Obtener datos de tipo Long
title: Obtención de datos largos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3a40bc3f4f65f747776d747d79868340de06f53
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429287"
---
# <a name="getting-long-data"></a>Obtener datos de tipo Long
Los DBMS definen *datos largos* como cualquier carácter o dato binario a lo largo de un determinado tamaño, como 255 caracteres. Estos datos pueden ser lo suficientemente pequeños como para almacenarse en un solo búfer, como una descripción de varios miles de caracteres. Sin embargo, puede que sea demasiado largo para almacenar en memoria, como documentos de texto largos o mapas de bits. Dado que estos datos no se pueden almacenar en un solo búfer, se recuperan del controlador en partes con **SQLGetData** después de que se hayan capturado los demás datos de la fila.  
  
> [!NOTE]  
>  En realidad, una aplicación puede recuperar cualquier tipo de datos con **SQLGetData**, no solo datos largos, aunque solo se pueden recuperar en partes los datos de caracteres y binarios. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un solo búfer, generalmente no hay ningún motivo para usar **SQLGetData**. Es mucho más fácil enlazar un búfer a la columna y dejar que el controlador devuelva los datos en el búfer.  
  
 Para recuperar datos de gran tamaño de una columna, una aplicación llama primero a **SQLFetchScroll** o **SQLFetch** para moverse a una fila y capturar los datos de las columnas enlazadas. A continuación, la aplicación llama a **SQLGetData**. **SQLGetData** tiene los mismos argumentos que **SQLBindCol**: un identificador de instrucción; un número de columna; el tipo de datos de C, la dirección y la longitud de bytes de una variable de aplicación; y la dirección de un búfer de longitud/indicador. Ambas funciones tienen los mismos argumentos porque realizan esencialmente la misma tarea: ambos describen una variable de aplicación para el controlador y especifican que los datos de una columna determinada se devuelvan en esa variable. Las principales diferencias son que se llama a **SQLGetData** después de capturar una fila (y a veces se conoce como *enlace en tiempo de ejecución* por este motivo) y que el enlace especificado por **SQLGetData** solo dura la duración de la llamada.  
  
 En cuanto a una sola columna, **SQLGetData** se comporta como **SQLFetch**: recupera los datos de la columna, los convierte al tipo de la variable de aplicación y lo devuelve en esa variable. También devuelve la longitud de bytes de los datos en el búfer de longitud/indicador. Para obtener más información sobre cómo devuelve **SQLFetch** los datos, vea [obtener una fila de datos](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** difiere de **SQLFetch** en un respeto importante. Si se llama más de una vez consecutivamente para la misma columna, cada llamada devuelve una parte sucesiva de los datos. Cada llamada a excepción de la última llamada devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos de cadena, truncados a la derecha). la última llamada devuelve SQL_SUCCESS. Así es como se usa **SQLGetData** para recuperar datos largos en partes. Cuando no hay más datos que devolver, **SQLGetData** devuelve SQL_NO_DATA. La aplicación es responsable de colocar los datos largos juntos, lo que podría significar la concatenación de las partes de los datos. Cada parte termina en null; la aplicación debe quitar el carácter de terminación NULL si se concatenan los elementos. La recuperación de datos en partes puede realizarse para los marcadores de longitud variable y para otros datos de gran tamaño. El valor devuelto en el búfer de longitud/indicador disminuye en cada llamada el número de bytes devueltos en la llamada anterior, aunque es común que el controlador no detecte la cantidad de datos disponibles y devuelva una longitud de bytes de SQL_NO_TOTAL. Por ejemplo:  
  
```  
// Declare a binary buffer to retrieve 5000 bytes of data at a time.  
SQLCHAR       BinaryPtr[5000];  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd, BinaryLenOrInd, NumBytes;  
SQLRETURN     rc;   
SQLHSTMT      hstmt;  
  
// Create a result set containing the ID and picture of each part.  
SQLExecDirect(hstmt, "SELECT PartID, Picture FROM Pictures", SQL_NTS);  
  
// Bind PartID to the PartID column.  
SQLBindCol(hstmt, 1, SQL_C_ULONG, &PartID, 0, &PartIDInd);  
  
// Retrieve and display each row of data.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // Display the part ID and initialize the picture.  
   DisplayID(PartID, PartIDInd);  
   InitPicture();  
  
   // Retrieve the picture data in parts. Send each part and the number   
   // of bytes in each part to a function that displays it. The number   
   // of bytes is always 5000 if there were more than 5000 bytes   
   // available to return (cbBinaryBuffer > 5000). Code to check if   
   // rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLGetData(hstmt, 2, SQL_C_BINARY, BinaryPtr, sizeof(BinaryPtr),  
                           &BinaryLenOrInd)) != SQL_NO_DATA) {  
      NumBytes = (BinaryLenOrInd > 5000) || (BinaryLenOrInd == SQL_NO_TOTAL) ?  
                  5000 : BinaryLenOrInd;  
      DisplayNextPictPart(BinaryPtr, NumBytes);  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 Existen varias restricciones en el uso de **SQLGetData**. Por lo general, las columnas a las que se tiene acceso con **SQLGetData**:  
  
-   Se debe tener acceso a en orden de número de columna creciente (debido al modo en que las columnas de un conjunto de resultados se leen desde el origen de datos). Por ejemplo, es un error llamar a **SQLGetData** para la columna 5 y, a continuación, llamarlo para la columna 4.  
  
-   No se puede enlazar.  
  
-   Debe tener un número de columna superior al de la última columna enlazada. Por ejemplo, si la última columna enlazada es la columna 3, es un error llamar a **SQLGetData** para la columna 2. Por este motivo, las aplicaciones deben asegurarse de colocar las columnas de datos largas al final de la lista de selección.  
  
-   No se puede usar si se llamó a **SQLFetch** o **SQLFetchScroll** para recuperar más de una fila. Para obtener más información, vea [usar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 Algunos controladores no aplican estas restricciones. Las aplicaciones interoperables deben suponer que existen o determinar qué restricciones no se aplican llamando a **SQLGetInfo** con la opción SQL_GETDATA_EXTENSIONS.  
  
 Si la aplicación no necesita todos los datos de una columna de datos binarios o de caracteres, puede reducir el tráfico de red en los controladores basados en DBMS estableciendo el atributo de instrucción SQL_ATTR_MAX_LENGTH antes de ejecutar la instrucción. Esto restringe el número de bytes de datos que se devolverán para cualquier carácter o columna binaria. Por ejemplo, supongamos que una columna contiene documentos de texto largo. Es posible que una aplicación que examina la tabla que contiene esta columna tenga que mostrar solo la primera página de cada documento. Aunque este atributo de instrucción se puede simular en el controlador, no hay ninguna razón para hacerlo. En concreto, si una aplicación desea truncar los datos de caracteres o binarios, debe enlazar un búfer pequeño a la columna con **SQLBindCol** y dejar que el controlador trunque los datos.
