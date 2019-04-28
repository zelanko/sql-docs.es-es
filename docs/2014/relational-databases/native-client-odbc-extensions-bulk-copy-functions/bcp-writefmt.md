---
title: bcp_writefmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_writefmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_writefmt function
ms.assetid: cb4c1d37-667d-4bcd-b13c-eb638bcc9b69
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d4a5067598b475ed8fe103606088d0e4d6d0554
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62689407"
---
# <a name="bcpwritefmt"></a>bcp_writefmt
  Crea un archivo de formato que contiene una descripción del formato del archivo de datos de la copia masiva actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_writefmt (  
HDBC   
hdbc  
,  
LPCTSTR   
szFormatFile  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *szFormatFile*  
 Es la ruta de acceso y nombre del archivo de usuario para recibir valores de formato para el archivo de datos.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 El archivo de formato especifica el formato de los datos de un archivo de datos creado mediante copia masiva. Las llamadas a [bcp_columns](bcp-columns.md) y [bcp_colfmt](bcp-colfmt.md) definen el formato del archivo de datos. **bcp_writefmt** guarda esta definición en el archivo al que se hace referencia en *szFormatFile*. Para obtener más información, vea [bcp_init](bcp-init.md).  
  
 Para obtener más información sobre la estructura de **bcp** archivos de formato de datos, vea [importar y exportar datos de forma masiva con la utilidad bcp &#40;SQL Server&#41;](../import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md).  
  
 Para cargar un archivo de formato guardado, use [bcp_readfmt](bcp-readfmt.md).  
  
> [!NOTE]  
>  El archivo de formato producido por **bcp_writefmt** solamente está admitido por las versiones de la utilidad **bcp** distribuida con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0 y posteriores.  
  
## <a name="example"></a>Ejemplo  
  
```  
// Variables like henv not specified.  
HDBC      hdbc;  
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
if (bcp_init(hdbc, _T("myTable"), _T("myData.csv"),  
   _T("myErrors"),    DB_OUT) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_columns(hdbc, 3) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
bcp_colfmt(hdbc, 1, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 1);  
bcp_colfmt(hdbc, 2, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 2);  
bcp_colfmt(hdbc, 3, SQLCHARACTER, 0, SQL_VARLEN_DATA, '\t', 1, 3);  
  
if (bcp_writefmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   printf_s("%ld rows copied from SQL Server\n", nRowsProcessed);  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
