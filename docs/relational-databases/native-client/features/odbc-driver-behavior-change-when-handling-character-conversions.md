---
title: Conversiones de char de control de cambios de ODBC
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 682a232a-bf89-4849-88a1-95b2fbac1467
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 82e9e3b1ed8487e864e91edfd3067f9fb97bbb71
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303841"
---
# <a name="odbc-driver-behavior-change-when-handling-character-conversions"></a>Cambio de comportamiento del controlador ODBC al administrar las conversiones de caracteres
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] controlador ODBC de Native Client (SQLNCLI11. dll) ha cambiado su funcionamiento de las conversiones SQL_WCHAR * (NCHAR/NVARCHAR/nvarchar (Max\* )) y SQL_CHAR (CHAR/VARCHAR/NARCHAR (Max)). Las funciones ODBC, como SQLGetData, SQLBindCol y SQLBindParameter, devuelven (-4) SQL_NO_TOTAL como el parámetro indicador de longitud al utilizar el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client. Las versiones anteriores del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client devolvían un valor de longitud, que puede ser incorrecto.  
  
## <a name="sqlgetdata-behavior"></a>Comportamiento de SQLGetData  
 Muchas funciones de Windows permiten especificar un tamaño de búfer de 0, siendo la longitud devuelta el tamaño de los datos devueltos. El patrón siguiente es frecuente para los programadores de Windows:  
  
```  
int iSize = 0;  
BYTE * pBuffer = NULL;  
GetMyFavoriteAPI(pBuffer, &iSize);   // Returns needed size in iSize  
pBuffer = new BYTE[iSize];   // Allocate buffer   
GetMyFavoriteAPI(pBuffer, &iSize);   // Retrieve actual data  
```  
  
 Sin embargo, no se debe utilizar **SQLGetData** en este escenario. No se debe utilizar el patrón siguiente:  
  
```  
// bad  
int iSize = 0;  
WCHAR * pBuffer = NULL;  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)0x1, 0, &iSize);   // Get storage size needed  
pBuffer = new WCHAR[(iSize/sizeof(WCHAR)) + 1];   // Allocate buffer  
SQLGetData(hstmt, SQL_W_CHAR, ...., (SQLPOINTER*)pBuffer, iSize, &iSize);   // Retrieve data  
```  
  
 Solo se puede llamar a **SQLGetData** para recuperar fragmentos de datos reales. No se admite el uso de **SQLGetData** para obtener el tamaño de los datos.  
  
 A continuación se muestra el impacto del cambio de controlador cuando se utiliza el patrón incorrecto. Esta aplicación consulta una columna **VARCHAR** y el enlace como Unicode (SQL_UNICODE/SQL_WCHAR):  
  
 Misma`select convert(varchar(36), '123')`  
  
```  
SQLGetData(hstmt, SQL_WCHAR, ....., (SQLPOINTER*) 0x1, 0 , &iSize);   // Attempting to determine storage size needed  
```  
  
|Versión del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client|Resultado de indicador o de longitud|Descripción|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client o anterior|6|El controlador suponía incorrectamente que la conversión de CHAR en WCHAR se podía conseguir como longitud * 2.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (versión 11.0.2100.60) o posterior|-4 (SQL_NO_TOTAL)|El controlador ya no supone que la conversión de CHAR a WCHAR o WCHAR a CHAR es una acción ( \*multiplicar) 2 o (dividir)/2.<br /><br /> Al llamar a **SQLGetData** ya no se devuelve la longitud de la conversión esperada. El controlador detecta la conversión a o desde CHAR y WCHAR y devuelve (-4) SQL_NO_TOTAL en lugar del comportamiento *2 o /2, que podría ser incorrecto.|  
  
 Use **SQLGetData** para recuperar los fragmentos de los datos. (Se muestra el pseudocódigo:)  
  
```  
while( (SQL_SUCCESS or SQL_SUCCESS_WITH_INFO) == SQLFetch(...) ) {  
   SQLNumCols(...iTotalCols...)  
   for(int iCol = 1; iCol < iTotalCols; iCol++) {  
      WCHAR* pBufOrig, pBuffer = new WCHAR[100];  
      SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get original chunk  
      while(NOT ALL DATA RETREIVED (SQL_NO_TOTAL, ...) ) {  
         pBuffer += 50;   // Advance buffer for data retrieved  
         // May need to realloc the buffer when you reach current size  
         SQLGetData(.... iCol ... pBuffer, 100, &iSize);   // Get next chunk  
      }  
   }  
}  
```  
  
## <a name="sqlbindcol-behavior"></a>Comportamiento de SQLBindCol  
 Misma`select convert(varchar(36), '1234567890')`  
  
```  
SQLBindCol(... SQL_W_CHAR, ...)   // Only bound a buffer of WCHAR[4] - Expecting String Data Right Truncation behavior  
```  
  
|Versión del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client|Resultado de indicador o de longitud|Descripción|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client o anterior|20|**SQLFetch** informa de que hay un truncamiento en el lado derecho de los datos.<br /><br /> La longitud es la longitud de los datos devueltos, no lo que se almacenó (se supone una conversión *2 de CHAR en WCHAR, lo que puede ser incorrecto para los glifos).<br /><br /> Los datos almacenados en el búfer son 123 \ 0. Se garantiza que el búfer está terminado en NULL.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (versión 11.0.2100.60) o posterior|-4 (SQL_NO_TOTAL)|**SQLFetch** informa de que hay un truncamiento en el lado derecho de los datos.<br /><br /> La longitud indica -4 (SQL_NO_TOTAL) debido a que el resto de los datos no se convirtió.<br /><br /> Los datos almacenados en el búfer son 123\0. - Se garantiza que el búfer está terminado en NULL.|  
  
## <a name="sqlbindparameter-output-parameter-behavior"></a>SQLBindParameter (comportamiento del parámetro OUTPUT)  
 Misma`create procedure spTest @p1 varchar(max) OUTPUT`  
  
 `select @p1 = replicate('B', 1234)`  
  
```  
SQLBindParameter(... SQL_W_CHAR, ...)   // Only bind up to first 64 characters  
```  
  
|Versión del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client|Resultado de indicador o de longitud|Descripción|  
|-----------------------------------------------------------------|---------------------------------|-----------------|  
|[!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] Native Client o anterior|2468|**SQLFetch** no devuelve más datos disponibles.<br /><br /> **SQLMoreResults** no devuelve más datos disponibles.<br /><br /> La longitud indica el tamaño de los datos devueltos desde el servidor, no el de los datos almacenados en el búfer.<br /><br /> El búfer original contiene 63 bytes y un terminador NULL. Se garantiza que el búfer está terminado en NULL.|  
|[!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client (versión 11.0.2100.60) o posterior|-4 (SQL_NO_TOTAL)|**SQLFetch** no devuelve más datos disponibles.<br /><br /> **SQLMoreResults** no devuelve más datos disponibles.<br /><br /> La longitud indica (-4) SQL_NO_TOTAL debido a que el resto de los datos no se convirtió.<br /><br /> El búfer original contiene 63 bytes y un terminador NULL. Se garantiza que el búfer está terminado en NULL.|  
  
## <a name="performing-char-and-wchar-conversions"></a>Realizar conversiones CHAR y WCHAR  
 El controlador ODBC de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client ofrece varias maneras de realizar las conversiones CHAR y WCHAR. La lógica es similar a la manipulación de blobs (varchar (Max), nvarchar (Max),...):  
  
-   Los datos se guardan o se truncan en el búfer especificado al enlazar con **SQLBindCol** o **SQLBindParameter**.  
  
-   Si no realiza el enlace, puede recuperar los datos en fragmentos mediante **SQLGetData** y **SQLParamData**.  
  
## <a name="see-also"></a>Consulte también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
