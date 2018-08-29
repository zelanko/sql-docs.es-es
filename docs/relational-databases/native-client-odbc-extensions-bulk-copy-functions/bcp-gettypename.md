---
title: bcp_gettypename | Microsoft Docs
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
- bcp_gettypename
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e00a0bc4178cc8ac607366e9d80377954c14d3ae
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43106166"
---
# <a name="bcpgettypename"></a>bcp_gettypename
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Devuelve el nombre del tipo SQL para un token del tipo BCP especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_gettypename (  
        INT token,  
        DBBOOL fIsMaxType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *símbolo (token)*  
 Valor que indica un token de tipo BCP.  
  
 *field*  
 Indica si el token solicitado es un tipo max.  
  
## <a name="returns"></a>Devuelve  
 Una cadena que contiene el nombre del tipo SQL que corresponde al tipo BCP. Si se especifica un tipo BCP no válido, se devuelve una cadena vacía.  
  
## <a name="remarks"></a>Notas  
 Los tokens de tipo BCP se definen en el archivo de encabezado sqlncli.h y en la biblioteca sqlncli11.lib.  
  
 La tabla siguiente especifica los posibles tipos BCP, tanto si son o no tipos max, y la salida esperada.  
  
|Nombre de tipo de BCP|MaxType|Salida|  
|-------------------|-------------|------------|  
|**SQLDECIMAL**|Antes o después|**decimal**|  
|**SQLNUMERIC**|Antes o después|**numeric**|  
|**SQLINT1**|Antes o después|**tinyint**|  
|**SQLINT2**|Antes o después|**smallint**|  
|**SQLINT4**|Antes o después|**int**|  
|**SQLMONEY**|Antes o después|**money**|  
|**SQLFLT8**|Antes o después|**float**|  
|**SQLDATETIME**|Antes o después|**datetime**|  
|**SQLBITN**|Antes o después|**bit null**|  
|**SQLBIT**|Antes o después|**bit**|  
|**SQLBIGCHAR**|no|**char**|  
|**SQLCHARACTER**|no|**char**|  
|**SQLBIGVARCHAR**|no|**varchar**|  
|**SQLVARCHAR**|no|**varchar**|  
|**SQLTEXT**|Antes o después|**texto**|  
|**SQLBIGBINARY**|no|**binario**|  
|**SQLBINARY**|no|**Binario**|  
|**SQLBIGVARBINARY**|no|**varbinary**|  
|**SQLVARBINARY**|no|**varbinary**|  
|**SQLIMAGE**|Antes o después|**Imagen**|  
|**SQLINTN**|Antes o después|**int null**|  
|**SQLDATETIMN**|Antes o después|**datetime-null**|  
|**SQLMONEYN**|Antes o después|**Money null**|  
|**SQLFLTN**|Antes o después|**float null**|  
|**SQLAOPSUM**|Antes o después|**Sum**|  
|**SQLAOPAVG**|Antes o después|**Avg**|  
|**SQLAOPCNT**|Antes o después|**Count**|  
|**SQLAOPMIN**|Antes o después|**Min**|  
|**SQLAOPMAX**|Antes o después|**Max**|  
|**SQLDATETIM4**|Antes o después|**smalldatetime**|  
|**SQLMONEY4**|Antes o después|**smallmoney**|  
|**SQLFLT4**|Antes o después|**real**|  
|**SQLUNIQUEID**|Antes o después|**uniqueidentifier**|  
|**SQLNCHAR**|no|**nchar**|  
|**SQLNVARCHAR**|no|**Nvarchar**|  
|**SQLNTEXT**|Antes o después|**ntext**|  
|**SQLVARIANT**|Antes o después|**sql_variant**|  
|**SQLINT8**|Antes o después|**Bigint**|  
|**SQLCHARACTER**|Sí|**ntext**|  
|**SQLBIGCHAR**|Sí|**ntext**|  
|**SQLBIGVARCHAR**|Sí|**ntext**|  
|**SQLVARCHAR**|Sí|**ntext**|  
|**SQLBINARY**|Sí|**varbinary(max)**|  
|**SQLBIGBINARY**|Sí|**varbinary(max)**|  
|**SQLBIGVARBINARY**|Sí|**varbinary(max)**|  
|**SQLVARBINARY**|Sí|**varbinary(max)**|  
|**SQLNCHAR**|Sí|**nvarchar(max)**|  
|**SQLNVARCHAR**|Sí|**nvarchar(max)**|  
|**SQLXML**|Sí|**Xml**|  
|**SQLUDT**|Antes o después|**UDT**|  
  
## <a name="bcpgettypename-support-for-enhanced-date-and-time-features"></a>bcp_gettypename admite las características mejoradas de fecha y hora  
 Se describen los valores de parámetro de token para los tipos de fecha y hora en la columna "Tipo en sqlncli.h" de la tabla en [cambios de copia masiva para tipos mejorada de fecha y hora &#40;OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). El valor devuelto está en la fila correspondiente de la columna " Tipo de almacenamiento de archivo".  
  
 Para obtener más información, consulte [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Vea también  
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
