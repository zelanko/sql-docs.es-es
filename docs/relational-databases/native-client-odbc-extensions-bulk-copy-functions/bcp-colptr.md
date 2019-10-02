---
title: bcp_colptr | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_colptr
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2dcc08890a230155c4ffefc3cf4a20dd72dd746f
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71707752"
---
# <a name="bcp_colptr"></a>bcp_colptr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Establece la dirección de datos de la variable de programa para la copia actual en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_colptr (  
        HDBC hdbc,  
        LPCBYTE pData,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *pData*  
 Es un puntero a los datos que van a copiarse. Si el tipo de datos enlazado es un tipo de valor grande (como SQLTEXT o SQLIMAGE), *pdata* puede ser null. Un *PDATA* null indica que los valores de datos largos se enviarán a SQL Server en fragmentos mediante [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md).  
  
 Si *pdata* se establece en NULL y la columna correspondiente al campo enlazado no es un tipo de valor grande, **bcp_colptr** produce un error.  
  
 Para obtener más información sobre los tipos de valores grandes, vea [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) **.**  
  
 *idxServerCol*  
 Es la posición ordinal de la columna en la tabla de base de datos en la que se copian los datos. La primera columna de una tabla es la columna 1. La posición ordinal de una columna se notifica mediante [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 La función **bcp_colptr** permite cambiar la dirección de los datos de origen de una columna determinada al copiar los datos en SQL Server con [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
 Inicialmente, el puntero a los datos de usuario se establece mediante una llamada a **bcp_bind**. Si la dirección de datos de la variable de programa cambia entre las llamadas a **bcp_sendrow**, puede llamar a **bcp_colptr** para restablecer el puntero a los datos. La siguiente llamada a **bcp_sendrow** envía los datos direccionados por la llamada a **bcp_colptr**.  
  
 Debe haber una llamada **bcp_colptr** independiente para cada columna de la tabla cuya dirección de datos desee modificar.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
