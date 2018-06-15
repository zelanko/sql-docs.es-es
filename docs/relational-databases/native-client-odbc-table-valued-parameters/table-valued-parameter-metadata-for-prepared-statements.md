---
title: Metadatos de parámetros con valores de tabla para instrucciones preparadas | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), metadata for prepared statements
ms.assetid: fd2fc705-2e98-4011-9822-c7e6cca4a535
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9dffa739b237de06d81d62c649c991e9bb54c775
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32948690"
---
# <a name="table-valued-parameter-metadata-for-prepared-statements"></a>Metadatos de parámetros con valores de tabla para instrucciones preparadas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Una aplicación puede obtener metadatos de una llamada a procedimiento preparada a través de SQLNumParams y SQLDescribeParam. Para los parámetros con valores de tabla, *DataTypePtr* está establecido en SQL_SS_TABLE. Metadatos adicionales están disponibles a través de SQLGetDescField para SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME y SQL_CA_SS_SCHEMA_NAME.  
  
 SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME y SQL_CA_SS_SCHEMA_NAME se pueden utilizar con SQLColumns para obtener los metadatos de columna para los tipos de tabla asociados con parámetros con valores de tabla. En este caso, SQL_SOPT_SS_NAME_SCOPE debe establecerse en SQL_SS_NAME_SCOPE_TABLE_TYPE antes de llamar a SQLColumns. A continuación, SQL_SOPT_SS_NAME_SCOPE se debe volver a establecer en el valor predeterminado, SQL_SS_NAME_SCOPE_TABLE, cuando la aplicación haya terminado de recuperar los metadatos de columnas de parámetros con valores de tabla.  
  
 SQL_CA_SS_TYPE_NAME, SQL_CA_SS_CATALOG_NAME y SQL_CA_SS_SCHEMA_NAME se pueden usar también con parámetros de tipos definidos por el usuario de CLR.  
  
 No puede obtener metadatos de parámetros con valores de tabla para instrucciones preparadas que no sean llamadas a procedimientos almacenados. Si lo intenta, la aplicación devuelve SQL_ERROR con SQLSTATE 42000 y el mensaje "error de sintaxis o infracción de acceso".  
  
## <a name="see-also"></a>Vea también  
 [Parámetros con valores de tabla &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md)  
  
  
