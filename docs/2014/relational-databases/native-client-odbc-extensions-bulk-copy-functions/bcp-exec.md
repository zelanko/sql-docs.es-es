---
title: bcp_exec | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_exec
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_exec function
ms.assetid: b23ea2cc-8545-4873-b0c1-57e76b0a3a7b
author: rothja
ms.author: jroth
ms.openlocfilehash: 8671ab15bc913917a558c9e1f90c15c0168e6cfc
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019506"
---
# <a name="bcp_exec"></a>bcp_exec
  Ejecuta una copia masiva completa de los datos entre una tabla de base de datos y un archivo de usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_exec (  
HDBC   
hdbc  
,  
LPDBINT   
pnRowsProcessed  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *pnRowsProcessed*  
 Es un puntero a un DBINT. La función **bcp_exec** llena este DBINT con el número de filas copiadas correctamente. Si *pnRowsProcessed* es NULL, **bcp_exec**lo omite.  
  
## <a name="returns"></a>Devoluciones  
 SUCCEED, SUCCEED_ASYNC o FAIL. La función **bcp_exce** devuleve SUCCEED si se se copian todas las filas. **bcp_exec** devuelve SUCCEED_ASYNC si la copia masiva asincrónica no se ha completado todavía. **bcp_exce** devuelve FAIL si se produce un error total o si el número de filas que generan errores alcanza el valor que se ha especificado para BCPMAXERRS con [bcp_control](bcp-control.md). BCPMAXERRS toma como valor predeterminado 10. La opción BCPMAXERRS afecta solo a los errores de sintaxis detectados por el proveedor al leer las filas del archivo de datos (y no las filas enviadas al servidor). El servidor anula el lote cuando detecta un error con una fila. Compruebe en el parámetro *pnRowsProcessed* el número de filas copiadas correctamente.  
  
## <a name="remarks"></a>Comentarios  
 Esta función copia los datos de un archivo de usuario en una tabla de base de datos o viceversa, dependiendo del valor del parámetro *eDirection* de [bcp_init](bcp-init.md).  
  
 Antes de llamar a **bcp_exec**, llame a **bcp_init** con un nombre de archivo de usuario válido. Si no lo hace, se producirá un error.  
  
 **bcp_exec** es la única función de copia masiva que es probable que quede pendiente durante un período de tiempo indeterminado. Por lo tanto, es la única función de copia masiva que admite el modo asincrónico. Para establecer el modo asincrónico, utilice [SQLSetConnectAttr](../native-client-odbc-api/sqlsetconnectattr.md) para establecer SQL_ATTR_ASYNC_ENABLE en SQL_ASYNC_ENABLE_ON antes de llamar a **bcp_exec**. Para comprobar si se ha completado, llame a **bcp_exec** con los mismos parámetros. Si la copia masiva no se ha completado todavía, **bcp_exec** devuelve SUCCEED_ASYNC. También devuelve en *pnRowsProcessed* un recuento del estado del número de filas enviadas al servidor. Las filas enviadas al servidor no se confirman hasta que se alcanza el final de un lote.  
  
 Para obtener información sobre un cambio importante en la copia masiva a partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , vea [realizar operaciones de copia masiva &#40;ODBC&#41;](../native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo, se muestra cómo utilizar **bcp_exec**:  
  
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
if (bcp_init(hdbc, _T("pubs..authors"), _T("authors.sav"), NULL, DB_OUT)  
   == FAIL)  
   {  
   // Raise error and return.  
   return;  
   }  
  
// Now, execute the bulk copy.   
if (bcp_exec(hdbc, &nRowsProcessed) == FAIL)  
   {  
   if (nRowsProcessed == -1)  
      {  
      printf_s("No rows processed on bulk copy execution.\n");  
      }  
   else  
      {  
      printf_s("Incomplete bulk copy.   Only %ld row%s copied.\n",  
         nRowsProcessed, (nRowsProcessed == 1) ? "": "s");  
      }  
   return;  
   }  
  
printf_s("%ld rows processed.\n", nRowsProcessed);  
  
// Carry on.  
```  
  
## <a name="see-also"></a>Consulte también  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
