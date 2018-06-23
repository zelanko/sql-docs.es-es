---
title: bcp_readfmt | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- bcp_readfmt
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_readfmt function
ms.assetid: 654001c8-ae9f-425c-b820-f0191bf89367
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 3d700f752a3194821065dc21ddd6ab96fa6a8f26
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200883"
---
# <a name="bcpreadfmt"></a>bcp_readfmt
  Lee una definición de formato de archivo de datos del archivo de formato especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_readfmt (  
HDBC   
hdbc  
,  
LPCTSTR   
szFormatFile  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *szFormatFile*  
 Es la ruta de acceso y nombre del archivo que contiene los valores de formato para el archivo de datos.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Notas  
 Después de `bcp_readfmt` lee los valores de formato, realiza las llamadas adecuadas a [bcp_columns](bcp-columns.md) y [bcp_colfmt](bcp-colfmt.md). No es necesario que analice un archivo de formato y realice estas llamadas.  
  
 Para conservar un archivo de formato, llame a [bcp_writefmt](bcp-writefmt.md). Las llamadas a `bcp_readfmt` pueden hacer referencia a formatos guardados. Para obtener más información, consulte [bcp_init](bcp-init.md).  
  
 Como alternativa, la utilidad de copia masiva (**bcp**) puede guardar formatos de datos definido por el usuario en archivos que pueden hacer referencia a `bcp_readfmt`. Para obtener más información sobre la **bcp** utilidad y la estructura de **bcp** archivos de formato de datos, vea [importación y exportación de datos &#40;SQL Server&#41;](../import-export/bulk-import-and-export-of-data-sql-server.md).  
  
 El `BCPDELAYREADFMT` valor de la *eOption* parámetro de [bcp_control](bcp-control.md) modifica el comportamiento de bcp_readfmt.  
  
> [!NOTE]  
>  La versión 4.2 o posterior de la utilidad **bcp** debe haber generado el archivo de formato.  
  
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
   _T("myErrors"),    DB_IN) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_readfmt(hdbc, _T("myFmtFile.fmt")) == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
if (bcp_exec(hdbc, &nRowsProcessed) == SUCCEED)  
   {  
   cout << nRowsProcessed << " rows copied to SQL Server\n";  
   }  
  
// Carry on.  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  