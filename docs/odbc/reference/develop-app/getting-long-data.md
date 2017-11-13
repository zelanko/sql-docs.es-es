---
title: Obtener datos de tipo Long | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- long data [ODBC]
- fetches [ODBC], long data
- result sets [ODBC], fetching
- SQLGetData function [ODBC], getting long data
- retrieving long data [ODBC]
ms.assetid: 6ccb44bc-8695-4bad-91af-363ef22bdb85
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0ea30c211e3cfd66acf1588ef9ca2a45fd1037d1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getting-long-data"></a>Obtener datos de tipo Long
Definen DBMS *datos long* como cualquier carácter o datos binarios a través de un determinado tamaño, por ejemplo, 255 caracteres. Estos datos pueden ser lo suficientemente pequeños como para almacenarse en un único búfer, como una descripción de la parte de varios miles de caracteres. Sin embargo, puede ser demasiado largo para almacenar en memoria, como documentos de texto largos o mapas de bits. Dado que estos datos no se puede almacenar en un único búfer, se recuperan desde el controlador en partes con **SQLGetData** después de que se hayan extraído los demás datos de la fila.  
  
> [!NOTE]  
>  Una aplicación puede en realidad se recupera cualquier tipo de datos con **SQLGetData**, no solo largos de datos, aunque se pueden recuperar sólo datos de caracteres y binarios en partes. Sin embargo, si los datos son lo suficientemente pequeños como para caber en un único búfer, no suele haber motivo para utilizar **SQLGetData**. Es mucho más fácil enlazar un búfer a la columna y dejar que el controlador de devolver los datos en el búfer.  
  
 Para recuperar datos de tipo long de una columna, una aplicación llama primero **SQLFetchScroll** o **SQLFetch** para desplazarse a una fila y capturar los datos de las columnas enlazadas. A continuación, la aplicación llama a **SQLGetData**. **SQLGetData** tiene los mismos argumentos que **SQLBindCol**: un identificador de instrucción; un número de columna; la longitud de bytes, la dirección y el tipo de datos de C de una variable de aplicación; y la dirección de un búfer de longitud/indicador. Ambas funciones tienen los mismos argumentos, ya que realizan básicamente la misma tarea: describen una variable de aplicación para el controlador y especificar que se deben devolver los datos de una determinada columna en esa variable. Las principales diferencias son que **SQLGetData** se llama después de que se captura una fila (y a veces se conoce como *enlace más tarde* por este motivo) y que el enlace especificado por **SQLGetData**  dura solo la duración de la llamada.  
  
 Con respecto a una sola columna, **SQLGetData** se comporta como **SQLFetch**: recupera los datos de la columna, lo convierte en el tipo de la variable de aplicación y lo devuelve en esa variable. También se devuelve la longitud de bytes de los datos en el búfer de longitud/indicador. Para obtener más información acerca de cómo **SQLFetch** devuelve datos, vea [capturar una fila de datos](../../../odbc/reference/develop-app/fetching-a-row-of-data.md).  
  
 **SQLGetData** difiere de **SQLFetch** en un aspecto importante. Si se llama varias veces seguidas por la misma columna, cada llamada devuelve una parte sucesivas de los datos. Cada llamada excepto la última llamada devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01004 (datos de cadena, derecho truncados); la última llamada devuelve SQL_SUCCESS. Se trata cómo **SQLGetData** se utiliza para recuperar datos largos en partes. Cuando no hay ningún dato más para devolver, **SQLGetData** devuelve SQL_NO_DATA. La aplicación es responsable de reunir los datos grandes, lo que podría significar la concatenación de las partes de los datos. Cada parte está terminada en null; la aplicación debe quitar el carácter de terminación null si las partes a concatenar. Recuperar datos en partes puede hacerse para marcadores de longitud variable, así como para otros datos de tipo long. El valor devuelto en las salidas de búfer de longitud/indicador en todas las llamadas por el número de bytes devueltos en la llamada anterior, aunque es común para el controlador que no se ha podido detectar la cantidad de datos disponibles y devolver una longitud de bytes de SQL_NO_TOTAL. Por ejemplo:  
  
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
  
 Hay varias restricciones sobre el uso de **SQLGetData**. Por lo general, acceso las columnas con **SQLGetData**:  
  
-   Debe tener acceso a en orden creciente de número de columna (debido a la manera en que las columnas del conjunto de resultados se leen desde el origen de datos). Por ejemplo, es un error llamar a **SQLGetData** para la columna 5 y, a continuación, llamar a para la columna 4.  
  
-   No se puede enlazar.  
  
-   Debe tener un número de columna mayor que la última columna enlazada. Por ejemplo, si la última columna enlazada es la columna 3, es un error llamar a **SQLGetData** para la columna 2. Por este motivo, las aplicaciones deben asegurarse colocar las columnas de datos de tipo long al final de la lista de selección.  
  
-   No se puede usar si **SQLFetch** o **SQLFetchScroll** se llamó para recuperar más de una fila. Para obtener más información, consulte [utilizar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md).  
  
 Algunos controladores no aplicar estas restricciones. Aplicaciones interoperables deben asumir que existen o para determinan qué restricciones no se aplican mediante una llamada a **SQLGetInfo** con la opción SQL_GETDATA_EXTENSIONS.  
  
 Si la aplicación no necesita todos los datos de un carácter o una columna de datos binarios, puede reducir el tráfico de red en los controladores basados en DBMS estableciendo el atributo de instrucción SQL_ATTR_MAX_LENGTH antes de ejecutar la instrucción. Así restringe el número de bytes de datos que se devolverán para cualquier carácter o columna binaria. Por ejemplo, suponga que una columna contiene texto largo documentos. Podría tener una aplicación que examina la tabla que contiene esta columna Mostrar solo la primera página de cada documento. Aunque puede simular este atributo de instrucción en el controlador, no hay ninguna razón para hacerlo. En concreto, si una aplicación desea truncar caracteres o datos binarios, se debe enlazar un búfer pequeño para la columna con **SQLBindCol** y dejar que el controlador truncar los datos.

