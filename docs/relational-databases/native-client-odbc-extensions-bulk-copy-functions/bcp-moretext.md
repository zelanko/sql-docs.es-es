---
title: bcp_moretext | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_moretext
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_moretext function
ms.assetid: 23e98015-a8e4-4434-9b3f-9c7350cf965f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 239bc3a5957c69e1262bf8229b6bdf85fae4ea67
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783423"
---
# <a name="bcp_moretext"></a>bcp_moretext
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Envía parte de un valor de tipo de datos largo, de longitud variable a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_moretext (  
        HDBC hdbc,  
        DBINT cbData,  
        LPCBYTE pData);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *cbData*  
 Es el número de bytes de datos que se copian en SQL Server a partir de los datos a los que se hace referencia en *pdata*. Un valor de SQL_NULL_DATA indica NULL.  
  
 *pData*  
 Es un puntero al fragmento de datos compatible, largo y de longitud variable que se va a enviar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="returns"></a>Devoluciones  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 Esta función se puede usar junto con [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) y [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md) para copiar valores de datos largos y de longitud variable en SQL Server en varios fragmentos más pequeños. **bcp_moretext** puede usarse con columnas que tienen los siguientes tipos de datos SQL Server: **Text**, **ntext**, **Image**, **VARCHAR (Max)**, **nvarchar (Max)**, **varbinary (Max)**, tipo definido por el usuario (UDT) y XML. **bcp_moretext** no admite conversiones de datos, los datos proporcionados deben coincidir con el tipo de datos de la columna de destino.  
  
 Si se llama a **bcp_bind** con un parámetro *pdata* no NULL para los tipos de datos admitidos por **bcp_moretext**, **bcp_sendrow** envía el valor de datos completo, independientemente de su longitud. Sin embargo, si **bcp_bind** tiene un parámetro *pdata* null para los tipos de datos admitidos, **bcp_moretext** se puede usar para copiar los datos inmediatamente después de una devolución correcta de **bcp_sendrow** que indica que se han procesado todas las columnas enlazadas con datos presentes.  
  
 Si usa **bcp_moretext** para enviar una columna de tipo de datos compatible en una fila, también debe utilizarla para enviar todas las demás columnas de tipos de datos compatibles de la fila. No se puede omitir ninguna columna. Los tipos de datos admitidos son SQLTEXT, SQLNTEXT, SQLIMAGE, SQLUDT y SQLXML. SQLCHARACTER, SQLVARCHAR, SQNCHAR, SQLBINARY y SQLVARBINARY también pertenecen a esta categoría si la columna es de tipo varchar (max), nvarchar (max) o varbinary (max), respectivamente.  
  
 Al llamar a **bcp_bind** o [bcp_collen](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-collen.md) se establece la longitud total de todas las partes de datos que se van a copiar en la columna SQL Server. Un intento de enviar SQL Server más bytes de los especificados en la llamada a **bcp_bind** o **bcp_collen** genera un error. Este error surgiría, por ejemplo, en una aplicación que usaba **bcp_collen** para establecer la longitud de los datos disponibles para una SQL Server columna de **texto** en 4500 y, a continuación, llamó a **bcp_moretext** cinco veces mientras se indica en cada llamada que la longitud del búfer de datos era de 1000 bytes.  
  
 Si una fila copiada contiene más de una columna de longitud variable larga, **bcp_moretext** primero envía sus datos a la columna con el número ordinal más bajo, seguida de la siguiente columna con el número ordinal más bajo, y así sucesivamente. Es importante una configuración correcta de la longitud total de datos esperados. No hay ninguna manera de indicar, fuera de la configuración de longitud, que la copia masiva ha recibido todos los datos de una columna.  
  
 Cuando los valores **var (Max)** se envían al servidor mediante bcp_sendrow y bcp_moretext, no es necesario llamar a bcp_collen para establecer la longitud de la columna. En su lugar, solo para estos tipos, el valor se termina llamando a bcp_sendrow con una longitud de cero.  
  
 Normalmente, una aplicación llama a **bcp_sendrow** y **bcp_moretext** en bucles para enviar varias filas de datos. A continuación se muestra un esquema de cómo hacerlo en una tabla que contiene dos columnas de **texto** :  
  
```  
while (there are still rows to send)  
{  
bcp_sendrow(...);  
  
for (all the data in the first varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
for (all the data in the second varbinary(max) column)  
bcp_moretext(...);  
bcp_moretext(hdbc, 0, NULL);  
  
}  
  
```  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se muestra cómo usar **bcp_moretext** con **bcp_bind** y **bcp_sendrow**:  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
DBINT      idRow = 5;  
char*      pPart1 = "This text value isn't very long,";  
char*      pPart2 = " but it's broken into three parts";  
char*      pPart3 = " anyhow.";  
DBINT      cbAllParts;  
DBINT      nRowsProcessed;  
  
// Application initiation, get an ODBC environment handle, allocate the  
// hdbc, and so on.  
...   
  
// Enable bulk copy prior to connecting on allocated hdbc.  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP, (SQLPOINTER) SQL_BCP_ON,  
   SQL_IS_INTEGER);  
  
// Connect to the data source, return on error.  
if (!SQL_SUCCEEDED(SQLConnect(hdbc, _T("myDSN"), SQL_NTS,  
   _T("myUser"), SQL_NTS, _T("myPwd"), SQL_NTS)))  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Initialize bulk copy.   
if (bcp_init(hdbc, "comdb..articles", NULL, NULL, DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Bind program variables to table columns.   
if (bcp_bind(hdbc, (LPCBYTE) &idRow, 0, SQL_VARLEN_DATA, NULL, 0,  
   SQLINT4, 1)    == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
cbAllParts = (DBINT) (strnlen(pPart1, sizeof(pPart1) + 1) + strnlen(pPart2, sizeof(pPart2) + 1) + strnlen(pPart3, sizeof(pPart3) + 1));  
if (bcp_bind(hdbc, NULL, 0, cbAllParts, NULL, 0, SQLTEXT, 2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Send this row, with the text value broken into three chunks.   
if (bcp_sendrow(hdbc) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart1, sizeof(pPart1) + 1), pPart1) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart2, sizeof(pPart2) + 1), pPart2) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
if (bcp_moretext(hdbc, (DBINT) strnlen(pPart3, sizeof(pPart3) + 1), pPart3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// All done. Get the number of rows processed (should be one).  
nRowsProcessed = bcp_done(hdbc);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>Consulte también  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
