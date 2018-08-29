---
title: bcp_exec | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_exec
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_exec function
ms.assetid: b23ea2cc-8545-4873-b0c1-57e76b0a3a7b
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2592a8a2b15369ecd15185cd3ccb9b9d6bd13356
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43078006"
---
# <a name="bcpexec"></a>bcp_exec
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ejecuta una copia masiva completa de los datos entre una tabla de base de datos y un archivo de usuario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_exec (  
        HDBC hdbc,  
        LPDBINT pnRowsProcessed);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *pnRowsProcessed*  
 Es un puntero a un DBINT. La función **bcp_exec** llena este DBINT con el número de filas copiadas correctamente. Si *pnRowsProcessed* es NULL, **bcp_exec**lo omite.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED, SUCCEED_ASYNC o FAIL. La función **bcp_exce** devuleve SUCCEED si se se copian todas las filas. **bcp_exec** devuelve SUCCEED_ASYNC si la copia masiva asincrónica no se ha completado todavía. **bcp_exec** devuelve FAIL si se produce un error total o si el número de filas que generan errores alcanza el valor especificado para BCPMAXERRS con [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md). BCPMAXERRS toma como valor predeterminado 10. La opción BCPMAXERRS afecta solo a los errores de sintaxis detectados por el proveedor al leer las filas del archivo de datos (y no las filas enviadas al servidor). El servidor anula el lote cuando detecta un error con una fila. Compruebe en el parámetro *pnRowsProcessed* el número de filas copiadas correctamente.  
  
## <a name="remarks"></a>Notas  
 Esta función copia los datos de un archivo de usuario a una tabla de base de datos o viceversa, dependiendo del valor de la *eDirection* parámetro [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md).  
  
 Antes de llamar a **bcp_exec**, llame a **bcp_init** con un nombre de archivo de usuario válido. Si no lo hace, se producirá un error.  
  
 **bcp_exec** es la única función de copia masiva que es probable que quede pendiente durante un período de tiempo indeterminado. Por lo tanto, es la única función de copia masiva que admite el modo asincrónico. Para establecer el modo asincrónico, utilice [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para establecer SQL_ATTR_ASYNC_ENABLE en SQL_ASYNC_ENABLE_ON antes de llamar a **bcp_exec**. Para comprobar si se ha completado, llame a **bcp_exec** con los mismos parámetros. Si la copia masiva no se ha completado todavía, **bcp_exec** devuelve SUCCEED_ASYNC. También devuelve en *pnRowsProcessed* un recuento del estado del número de filas enviadas al servidor. Las filas enviadas al servidor no se confirman hasta que se alcanza el final de un lote.  
  
 Para obtener información sobre una separación de cambio de copia masiva a partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], consulte [realizar operaciones de copia masiva &#40;ODBC&#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
