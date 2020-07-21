---
title: bcp_gettypename | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_gettypename
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_gettypename function
ms.assetid: 65f036d1-f60e-4b8a-97b3-76fccf0dfed4
author: rothja
ms.author: jroth
ms.openlocfilehash: 0341d9ba11cd66fdbfb72a05521028098c56c400
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019444"
---
# <a name="bcp_gettypename"></a>bcp_gettypename
  Devuelve el nombre del tipo SQL para un token del tipo BCP especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RETCODE bcp_gettypename (  
INT   
token  
,  
DBBOOL   
fIsMaxType  
);  
  
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
|`SQLDECIMAL`|Es posible usar el|**decimal**|  
|`SQLNUMERIC`|Es posible usar el|**numeric**|  
|`SQLINT1`|Es posible usar el|**tinyint**|  
|`SQLINT2`|Es posible usar el|**smallint**|  
|`SQLINT4`|Es posible usar el|**int**|  
|`SQLMONEY`|Es posible usar el|**money**|  
|`SQLFLT8`|Es posible usar el|**float**|  
|`SQLDATETIME`|Es posible usar el|**datetime**|  
|`SQLBITN`|Es posible usar el|**bit-null**|  
|`SQLBIT`|Es posible usar el|**bit**|  
|`SQLBIGCHAR`|No|**char**|  
|`SQLCHARACTER`|No|**char**|  
|`SQLBIGVARCHAR`|No|**varchar**|  
|`SQLVARCHAR`|No|**varchar**|  
|`SQLTEXT`|Es posible usar el|**text**|  
|`SQLBIGBINARY`|No|**binary**|  
|`SQLBINARY`|No|**Binario**|  
|`SQLBIGVARBINARY`|No|**Varbinary**|  
|`SQLVARBINARY`|No|**Varbinary**|  
|`SQLIMAGE`|Es posible usar el|**Imagen**|  
|`SQLINTN`|Es posible usar el|**int-null**|  
|`SQLDATETIMN`|Es posible usar el|**datetime-null**|  
|`SQLMONEYN`|Es posible usar el|**money-null**|  
|`SQLFLTN`|Es posible usar el|**float-null**|  
|`SQLAOPSUM`|Es posible usar el|**Sume**|  
|`SQLAOPAVG`|Es posible usar el|**Latencia**|  
|`SQLAOPCNT`|Es posible usar el|**Recuento**|  
|`SQLAOPMIN`|Es posible usar el|**Minuto**|  
|`SQLAOPMAX`|Es posible usar el|**Máx.**|  
|`SQLDATETIM4`|Es posible usar el|**smalldatetime**|  
|`SQLMONEY4`|Es posible usar el|**Smallmoney**|  
|`SQLFLT4`|Es posible usar el|**Impuestos**|  
|`SQLUNIQUEID`|Es posible usar el|**uniqueidentifier**|  
|`SQLNCHAR`|No|**Nchar**|  
|`SQLNVARCHAR`|No|**Nvarchar**|  
|`SQLNTEXT`|Es posible usar el|**Ntext**|  
|`SQLVARIANT`|Es posible usar el|**sql_variant**|  
|`SQLINT8`|Es posible usar el|**BIGINT**|  
|`SQLCHARACTER`|Yes|**ntext**|  
|`SQLBIGCHAR`|Yes|**ntext**|  
|`SQLBIGVARCHAR`|Yes|**ntext**|  
|`SQLVARCHAR`|Yes|**ntext**|  
|`SQLBINARY`|Yes|**varbinary(max)**|  
|`SQLBIGBINARY`|Yes|**varbinary(max)**|  
|`SQLBIGVARBINARY`|Yes|**varbinary(max)**|  
|`SQLVARBINARY`|Yes|**varbinary(max)**|  
|`SQLNCHAR`|Yes|**nvarchar(max)**|  
|`SQLNVARCHAR`|Yes|**nvarchar(max)**|  
|`SQLXML`|Yes|**Lenguaje**|  
|`SQLUDT`|Es posible usar el|**Definido**|  
  
## <a name="bcp_gettypename-support-for-enhanced-date-and-time-features"></a>bcp_gettypename admite las características mejoradas de fecha y hora  
 Los valores de los parámetros de token para los tipos de fecha y hora se describen en la columna "Type in SQLNCLI. h" de la tabla en [cambios de copia masiva para los tipos de fecha y hora mejorados &#40;OLE DB y ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md). El valor devuelto está en la fila correspondiente de la columna " Tipo de almacenamiento de archivo".  
  
 Para obtener más información, vea [mejoras de fecha y hora &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="see-also"></a>Consulte también  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
