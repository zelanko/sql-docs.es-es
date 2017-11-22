---
title: bcp_colptr | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
apiname: bcp_colptr
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_colptr function
ms.assetid: 02ece13e-1da3-4f9d-b860-3177e43d2471
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1ddc9f3139136383e5a4f37b827f6d2c12ecf2c5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="bcpcolptr"></a>bcp_colptr
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
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *pData*  
 Es un puntero a los datos que van a copiarse. Si el tipo de datos enlazado es el tipo de valor grande (como SQLTEXT o SQLIMAGE), *pData* puede ser NULL. Un valor NULL *pData* indica valores de datos largos se enviarán a SQL Server en fragmentos utilizando [bcp_moretext](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-moretext.md).  
  
 Si *pData* se establece en NULL y la columna correspondiente al campo enlazado no es un tipo de valor grande, **bcp_colptr** se produce un error.  
  
 Para obtener más información sobre los tipos de valores grandes, consulte [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)**.**  
  
 *idxServerCol*  
 Es la posición ordinal de la columna en la tabla de base de datos en la que se copian los datos. La primera columna de una tabla es la columna 1. La posición ordinal de una columna se notifica mediante [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 El **bcp_colptr** función le permite cambiar la dirección de origen de datos de una determinada columna al copiar los datos a SQL Server con [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
 Inicialmente, el puntero a los datos de usuario se establece mediante una llamada a **bcp_bind**. Si cambia la dirección de datos de la variable de programa entre las llamadas a **bcp_sendrow**, puede llamar a **bcp_colptr** para restablecer el puntero a los datos. La siguiente llamada a **bcp_sendrow** envía los datos dirigidos por la llamada a **bcp_colptr**.  
  
 Debe haber un independiente **bcp_colptr** llamada para cada columna en la tabla cuya dirección de datos desea modificar.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
