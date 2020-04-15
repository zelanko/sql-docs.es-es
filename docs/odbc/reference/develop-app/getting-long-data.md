---
title: Obtención de datos largos ? Microsoft Docs
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
ms.openlocfilehash: da901c22eb26af063397b4af184179ebe5c75924
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298995"
---
# <a name="getting-long-data"></a>Obtener datos de tipo Long
Los DBMS definen *datos largos* como cualquier carácter o datos binarios de un tamaño determinado, como 255 caracteres. Estos datos pueden ser lo suficientemente pequeños como para almacenarse en un único búfer, como una descripción de parte de varios miles de caracteres. Sin embargo, puede ser demasiado largo para almacenar en la memoria, como documentos de texto largo o mapas de bits. Dado que estos datos no se pueden almacenar en un único búfer, se recuperan del controlador en partes con **SQLGetData** después de que se hayan capturado los demás datos de la fila.  
  
> [!NOTE]  
>  Una aplicación realmente puede recuperar cualquier tipo de datos con **SQLGetData**, no solo datos largos, aunque solo se pueden recuperar datos binarios y de caracteres en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un único búfer, generalmente no hay ninguna razón para usar **SQLGetData**. Es mucho más fácil enlazar un búfer a la columna y dejar que el controlador devuelva los datos en el búfer.  
  
 Para recuperar datos largos de una columna, una aplicación llama primero **SQLFetchScroll** o **SQLFetch** para mover a una fila y capturar los datos de las columnas enlazadas. A continuación, la aplicación llama a **SQLGetData**. **SQLGetData** tiene los mismos argumentos que **SQLBindCol**: un identificador de instrucción; un número de columna; el tipo de datos C, la dirección y la longitud de bytes de una variable de aplicación; y la dirección de un búfer de longitud/indicador. Ambas funciones tienen los mismos argumentos porque realizan esencialmente la misma tarea: ambas describen una variable de aplicación para el controlador y especifican que los datos de una columna determinada deben devolverse en esa variable. Las principales diferencias son que **SQLGetData** se llama después de recuperar una fila (y a veces se conoce como *enlace en tiempo de ejecución* por este motivo) y que el enlace especificado por **SQLGetData** dura solo durante la duración de la llamada.  
  
 En cuanto a una sola columna, **SQLGetData** se comporta como **SQLFetch:** recupera los datos de la columna, los convierte en el tipo de la variable de aplicación y los devuelve en esa variable. También devuelve la longitud de bytes de los datos en el búfer de longitud/indicador. Para obtener más información acerca de cómo **SQLFetch** devuelve datos, vea [Obtener una fila de datos](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** difiere de **SQLFetch** en un aspecto importante. Si se llama más de una vez consecutivamente para la misma columna, cada llamada devuelve una parte sucesiva de los datos. Cada llamada excepto la última llamada devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos de cadena, truncados a la derecha); la última llamada devuelve SQL_SUCCESS. Así es como **SQLGetData** se usa para recuperar datos largos en partes. Cuando no hay más datos que devolver, **SQLGetData** devuelve SQL_NO_DATA. La aplicación es responsable de juntar los datos largos, lo que podría significar concatenar las partes de los datos. Cada parte está terminada en null; la aplicación debe quitar el carácter de terminación nula si concatena las partes. La recuperación de datos en partes se puede hacer para marcadores de longitud variable, así como para otros datos largos. El valor devuelto en el búfer de longitud/indicador disminuye en cada llamada por el número de bytes devueltos en la llamada anterior, aunque es común que el controlador no pueda detectar la cantidad de datos disponibles y devolver una longitud de bytes de SQL_NO_TOTAL. Por ejemplo:  
  
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
  
 Existen varias restricciones en el uso de **SQLGetData**. Por lo general, las columnas a las que se tiene acceso con **SQLGetData:**  
  
-   Se debe tener acceso en orden de aumento del número de columna (debido a la forma en que las columnas de un conjunto de resultados se leen desde el origen de datos). Por ejemplo, es un error llamar a **SQLGetData** para la columna 5 y, a continuación, llamarlo para la columna 4.  
  
-   No se puede enlazar.  
  
-   Debe tener un número de columna mayor que la última columna enlazada. Por ejemplo, si la última columna enlazada es la columna 3, es un error llamar a **SQLGetData** para la columna 2. Por este motivo, las aplicaciones deben asegurarse de colocar columnas de datos largas al final de la lista de selección.  
  
-   No se puede usar si **SQLFetch** o **SQLFetchScroll** se llamó para recuperar más de una fila. Para obtener más información, consulte Uso de [cursores](../../../odbc/reference/develop-app/using-block-cursors.md)de bloque .  
  
 Algunos conductores no aplican estas restricciones. Las aplicaciones interoperables deben suponer que existen o determinar qué restricciones no se aplican llamando a **SQLGetInfo** con la opción SQL_GETDATA_EXTENSIONS.  
  
 Si la aplicación no necesita todos los datos de un carácter o columna de datos binarios, puede reducir el tráfico de red en controladores basados en DBMS estableciendo el atributo de instrucción SQL_ATTR_MAX_LENGTH antes de ejecutar la instrucción. Esto restringe el número de bytes de datos que se devolverán para cualquier carácter o columna binaria. Por ejemplo, supongamos que una columna contiene documentos de texto largo. Una aplicación que examina la tabla que contiene esta columna podría tener que mostrar solo la primera página de cada documento. Aunque este atributo de instrucción se puede simular en el controlador, no hay ninguna razón para hacerlo. En particular, si una aplicación desea truncar caracteres o datos binarios, debe enlazar un pequeño búfer a la columna con **SQLBindCol** y dejar que el controlador truncalos.
