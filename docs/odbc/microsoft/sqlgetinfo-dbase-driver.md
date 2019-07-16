---
title: SQLGetInfo (dBASE controlador) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLGetInfo
ms.assetid: 42ffdc9c-281b-4df5-ac6d-7b34f15ecd4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ba029c2f75fc715b1286a950cf11c1658bdab35
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003295"
---
# <a name="sqlgetinfo-dbase-driver"></a>SQLGetInfo (dBASE controlador)
> [!NOTE]  
>  Este tema proporciona información específica del controlador de dBASE. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** es compatible con el tipo de información SQL_FILE_USAGE. El valor devuelto es un entero de 16 bits que indica el modo en que el controlador trata directamente los archivos en un origen de datos:  
  
-   SQL_FILE_NOT_SUPPORTED - el controlador no es un controlador de nivel único.  
  
-   SQL_FILE_TABLE - un controlador de nivel único trata los archivos de origen de datos como tablas.  
  
-   SQL_FILE_QUALIFIER - un controlador de nivel único trata los archivos en un origen de datos como un calificador.  
  
 El controlador ODBC devuelve SQL_FILE_TABLE porque cada archivo es una tabla.  
  
## <a name="sqlaltertable"></a>SQL_ALTER_TABLE  
 SQL_AT_ADD_COLUMN &#124; SQL_AT_DROP_COLUMN  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|`Version`|Formato de números de versión|  
|----------|-------------|-------------------------------|  
|DBASE|3.0|03.00.0000|  
||4.0|04.00.0000|  
||5.0|05.00.0000|  
  
## <a name="sqlddlindex"></a>SQL_DDL_INDEX  
 SQL_DL_CREATE_INDEX  
  
 SQL_DL_DROP_INDEX  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION &#124; SQL_QU_INDEX_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
