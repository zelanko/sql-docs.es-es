---
description: SQLGetInfo (controlador de Paradox)
title: SQLGetInfo (controlador de Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], Paradox Driver
ms.assetid: 43aab762-68f4-4128-b8f5-8878ea5f1258
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c158c2d2afe7218bc6dd92666e3378381c9b2985
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421749"
---
# <a name="sqlgetinfo-paradox-driver"></a>SQLGetInfo (controlador de Paradox)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de Paradox. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** admite el tipo de información SQL_FILE_USAGE. El valor devuelto es un entero de 16 bits que indica cómo el controlador trata directamente los archivos de un origen de datos:  
  
-   SQL_FILE_NOT_SUPPORTED: el controlador no es un controlador de un solo nivel.  
  
-   SQL_FILE_TABLE: un controlador de un solo nivel trata los archivos de un origen de datos como tablas.  
  
-   SQL_FILE_QUALIFIER: un controlador de un solo nivel trata los archivos de un origen de datos como un calificador.  
  
 El controlador ODBC devuelve SQL_FILE_TABLE porque cada archivo es una tabla.  
  
## <a name="sql_alter_table"></a>SQL_ALTER_TABLE  
 SQL_AT_ADD_COLUMN &#124; SQL_AT_DROP_COLUMN  
  
## <a name="sql_ddl_index"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|Versión|Formato de los números de versión|  
|----------|-------------|-------------------------------|  
|Paradox|3.x|03.00.0000|  
||4.x|04.00.0000|  
||x|05.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION &#124; SQL_QU_INDEX_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
