---
title: bcp_collen | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_collen
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_collen function
ms.assetid: faaf1f7a-81f2-4852-a178-56602c33673a
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e3b1a42cf9ec888e3cf5bbb265eb0f42c5ecc0c8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895711"
---
# <a name="bcpcollen"></a>bcp_collen
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Establece la longitud de los datos de la variable del programa para la copia masiva actual en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_collen (  
        HDBC hdbc,  
        DBINT cbData,  
        INT idxServerCol);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
 *cbData*  
 Es la longitud de los datos de la variable del programa; no incluye la longitud del indicador ni del terminador de longitud. Si se establece *cbData* en SQL_NULL_DATA, se indica que todas las filas copiadas en el servidor contienen un valor NULL para la columna. Si se establece en SQL_VARLEN_DATA, se indica que se utiliza un terminador de cadena u otro método para determinar la longitud de los datos copiados. Si hay un indicador y un terminador de longitud, el sistema utiliza el que permita que se copien menos datos.  
  
 *idxServerCol*  
 Es la posición ordinal de la columna en la tabla en la que se copian los datos. La primera columna es 1. La posición ordinal de una columna se notifica mediante [SQLColumns](../../relational-databases/native-client-odbc-api/sqlcolumns.md).  
  
## <a name="returns"></a>Devuelve  
 SUCCEED o FAIL.  
  
## <a name="remarks"></a>Comentarios  
 La función **bcp_collen** permite cambiar la longitud de los datos en la variable del programa para una determinada columna al copiar los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
 La longitud de los datos se determina inicialmente cuando se llama a [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) . Si la longitud de los datos cambia entre las llamadas a **bcp_sendrow** y no se utiliza ningún prefijo o terminador de longitud, puede llamar a **bcp_collen** para restablecer la longitud. La llamada siguiente a **bcp_sendrow** utiliza la longitud establecida por la llamada a **bcp_collen**.  
  
 Debe llamar una vez a **bcp_collen** para cada columna de la tabla cuya longitud de los datos desee modificar.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
