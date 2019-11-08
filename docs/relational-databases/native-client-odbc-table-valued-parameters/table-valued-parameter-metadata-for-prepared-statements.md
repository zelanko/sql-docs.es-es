---
title: Metadatos de parámetros con valores de tabla para instrucciones preparadas | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 17b96f9a18e2b076bda76550b8796301f815c9f5
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73790734"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>Metadatos de parámetros con valores de tabla para instrucciones preparadas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Una aplicación puede obtener metadatos para una llamada a procedimiento preparada a través de SQLNumParams y SQLDescribeParam. En el caso de los parámetros con valores de tabla, *DataTypePtr* se establece en SQL_SS_TABLE. Los metadatos adicionales están disponibles a través de SQLGetDescField para SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME y SQL_CA_SS_SCHEMA_NAME.  
  
 SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME y SQL_CA_SS_SCHEMA_NAME se pueden usar con SQLColumns para obtener los metadatos de columna para los tipos de tabla asociados a los parámetros con valores de tabla. En este caso, SQL_SOPT_SS_NAME_SCOPE debe establecerse en SQL_SS_NAME_SCOPE_TABLE_TYPE antes de que se llame a SQLColumns. A continuación, SQL_SOPT_SS_NAME_SCOPE se debe volver a establecer en el valor predeterminado, SQL_SS_NAME_SCOPE_TABLE, cuando la aplicación haya terminado de recuperar los metadatos de columnas de parámetros con valores de tabla.  
  
 SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME y SQL_CA_SS_SCHEMA_NAME se pueden usar también con parámetros de tipos definidos por el usuario de CLR.  
  
 No puede obtener metadatos de parámetros con valores de tabla para instrucciones preparadas que no sean llamadas a procedimientos almacenados. Si lo intenta, la aplicación devuelve SQL_ERROR con SQLSTATE 42000 y el mensaje "error de sintaxis o infracción de acceso".  
  
## <a name="see-also"></a>Vea también  
 [Parámetros &#40;con valores de tabla ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
