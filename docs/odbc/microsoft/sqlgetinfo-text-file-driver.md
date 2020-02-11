---
title: SQLGetInfo (controlador de archivo de texto) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetInfo function [ODBC], Text File Driver
- text file driver [ODBC], SQLGetInfo
ms.assetid: 6b7a630e-47f8-4ee1-b2a7-476bc1d0b0d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 892fdabc319b1d495120cdce20d77f05cd232418
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898830"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** admite el tipo de información SQL_FILE_USAGE. El valor devuelto es un entero de 16 bits que indica cómo el controlador trata directamente los archivos de un origen de datos:  
  
-   SQL_FILE_NOT_SUPPORTED: el controlador no es un controlador de un solo nivel.  
  
-   SQL_FILE_TABLE: un controlador de un solo nivel trata los archivos de un origen de datos como tablas.  
  
-   SQL_FILE_QUALIFIER: un controlador de un solo nivel trata los archivos de un origen de datos como un calificador.  
  
 El controlador ODBC devuelve SQL_FILE_TABLE para Textdriver, porque cada archivo es una tabla.  
  
## <a name="sql_dbms_ver"></a>SQL_DBMS_VER  
  
|ISAM|Versión|Formato de los números de versión|  
|----------|-------------|-------------------------------|  
|Texto|1.0|01.00.0000|  
  
## <a name="sql_catalog_usage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sql_timedate_functions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &#124; SQL_FN_TD_CURTIME &#124; SQL_FN_TD_DAYOFMONTH &#124; SQL_FN_TD_DAYOFWEEK &#124; SQL_FN_TD_DAYOFYEAR &#124; SQL_FN_TD_HOUR &#124; SQL_FN_TD_MINUTE &#124; SQL_FN_TD_MONTH &#124; SQL_FN_TD_NOW &#124; SQL_FN_TD_SECOND &#124; SQL_FN_TD_WEEK &#124; SQL_FN_TD_YEAR
