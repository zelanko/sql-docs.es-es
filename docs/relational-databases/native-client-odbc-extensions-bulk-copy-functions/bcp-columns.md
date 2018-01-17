---
title: bcp_columns | Microsoft Docs
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
apiname: bcp_columns
apilocation: sqlncli11.dll
apitype: DLLExport
helpviewer_keywords: bcp_columns function
ms.assetid: 5376f6fe-9508-439a-8c66-778d77f19ac3
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4b48c2c0953e3565a406bf2a22788a2e1c537110
ms.sourcegitcommit: 779f3398e4e3f4c626d81ae8cedad153bee69540
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/16/2018
---
# <a name="bcpcolumns"></a>bcp_columns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Establece el número total de columnas del archivo de usuario para su uso con una copia masiva a o de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [bcp_setbulkmode](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-setbulkmode.md) puede usarse en lugar de bcp_columns y [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_columns (  
        HDBC hdbc,  
        INT nColumns);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *nColumns*  
 Es el número total de columnas en el archivo de usuario. Incluso si se está preparando para la copia masiva de datos del archivo de usuario para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tabla y no desea copiar todas las columnas del archivo de usuario, debe establecer *nColumns* al número total de columnas del archivo de usuario.  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 Esta función se puede llamar solo después [bcp_init](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-init.md) se ha llamado con un nombre de archivo válido.  
  
 Solo debe llamar a esta función si piensa utilizar un formato de archivo de usuario que difiere del valor predeterminado. Para obtener más información acerca de la descripción del formato predeterminado del archivo de usuario, consulte **bcp_init**.  
  
 Después de llamar a **bcp_columns**, debe llamar a [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md) para cada columna en el archivo de usuario para definir completamente un formato de archivo personalizado.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
