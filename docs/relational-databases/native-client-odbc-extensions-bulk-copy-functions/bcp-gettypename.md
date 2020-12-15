---
description: bcp_gettypename
title: bcp_gettypename | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- bcp_gettypename
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3872736a1748dbd06e251a65d358522e7b92a630
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97483377"
---
# <a name="bcp_gettypename"></a>bcp_gettypename
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Devuelve el nombre del tipo SQL para un token del tipo BCP especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_gettypename (  
        INT token,  
        DBBOOL fIsMaxType);  
```  
  
## <a name="arguments"></a>Argumentos  
 *token*  
 Valor que indica un token de tipo BCP.  
  
 *campo*  
 Indica si el token solicitado es un tipo max.  
  
## <a name="returns"></a>Devoluciones  
 Una cadena que contiene el nombre del tipo SQL que corresponde al tipo BCP. Si se especifica un tipo BCP no válido, se devuelve una cadena vacía.  
  
## <a name="remarks"></a>Comentarios  
 Los tokens de tipo BCP se definen en el archivo de encabezado sqlncli.h y en la biblioteca sqlncli11.lib.  
  
 La tabla siguiente especifica los posibles tipos BCP, tanto si son o no tipos max, y la salida esperada.  
  
|Nombre de tipo de BCP|MaxType|Resultados|  
|-------------------|-------------|------------|  
|**SQLDECIMAL**|Es posible usar el|**decimal**|  
|**SQLNUMERIC**|Es posible usar el|**numeric**|  
|**SQLINT1**|Es posible usar el|**tinyint**|  
|**SQLINT2**|Es posible usar el|**smallint**|  
|**SQLINT4**|Es posible usar el|**int**|  
|**SQLMONEY**|Es posible usar el|**money**|  
|**SQLFLT8**|Es posible usar el|**float**|  
|**SQLDATETIME**|Es posible usar el|**datetime**|  
|**SQLBITN**|Es posible usar el|**bit-null**|  
|**SQLBIT**|Es posible usar el|**bit**|  
|**SQLBIGCHAR**|No|**char**|  
|**SQLCHARACTER**|No|**char**|  
|**SQLBIGVARCHAR**|No|**varchar**|  
|**SQLVARCHAR**|No|**varchar**|  
|**SQLTEXT**|Es posible usar el|**text**|  
|**SQLBIGBINARY**|No|**binary**|  
|**SQLBINARY**|No|**Binario**|  
|**SQLBIGVARBINARY**|No|**Varbinary**|  
|**SQLVARBINARY**|No|**Varbinary**|  
|**SQLIMAGE**|Es posible usar el|**Imagen**|  
|**SQLINTN**|Es posible usar el|**int-null**|  
|**SQLDATETIMN**|Es posible usar el|**datetime-null**|  
|**SQLMONEYN**|Es posible usar el|**money-null**|  
|**SQLFLTN**|Es posible usar el|**float-null**|  
|**SQLAOPSUM**|Es posible usar el|**Sum**|  
|**SQLAOPAVG**|Es posible usar el|**Avg**|  
|**SQLAOPCNT**|Es posible usar el|**Count**|  
|**SQLAOPMIN**|Es posible usar el|**Mín.**|  
|**SQLAOPMAX**|Es posible usar el|**Máx.**|  
|**SQLDATETIM4**|Es posible usar el|**smalldatetime**|  
|**SQLMONEY4**|Es posible usar el|**Smallmoney**|  
|**SQLFLT4**|Es posible usar el|**Impuestos**|  
|**SQLUNIQUEID**|Es posible usar el|**uniqueidentifier**|  
|**SQLNCHAR**|No|**Nchar**|  
|**SQLNVARCHAR**|No|**Nvarchar**|  
|**SQLNTEXT**|Es posible usar el|**Ntext**|  
|**SQLVARIANT**|Es posible usar el|**sql_variant**|  
|**SQLINT8**|Es posible usar el|**Bigint**|  
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
|**SQLUDT**|Es posible usar el|**Definido**|  
  
## <a name="bcp_gettypename-support-for-enhanced-date-and-time-features"></a>bcp_gettypename admite las características mejoradas de fecha y hora  
 Los valores de los parámetros de token para los tipos de fecha y hora se describen en la columna "Type in SQLNCLI. h" de la tabla en [cambios de copia masiva para los tipos de fecha y hora mejorados &#40;OLE DB y ODBC&#41;](../../relational-databases/native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). El valor devuelto está en la fila correspondiente de la columna " Tipo de almacenamiento de archivo".  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
