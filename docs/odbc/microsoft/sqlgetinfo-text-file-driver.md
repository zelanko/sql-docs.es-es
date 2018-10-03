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
manager: craigg
ms.openlocfilehash: 37d8d67300ec29a2b346f5f6b958c1955d08db0a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792173"
---
# <a name="sqlgetinfo-text-file-driver"></a>SQLGetInfo (controlador de archivo de texto)
> [!NOTE]  
>  En este tema se proporciona información específica del controlador de archivo de texto. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 **SQLGetInfo** es compatible con el tipo de información SQL_FILE_USAGE. El valor devuelto es un entero de 16 bits que indica el modo en que el controlador trata directamente los archivos en un origen de datos:  
  
-   SQL_FILE_NOT_SUPPORTED: El controlador no es un controlador de nivel único.  
  
-   SQL_FILE_TABLE: Un controlador de nivel único trata los archivos de origen de datos como tablas.  
  
-   SQL_FILE_QUALIFIER: Un controlador de nivel único trata los archivos en un origen de datos como un calificador.  
  
 El controlador ODBC devuelve SQL_FILE_TABLE para el Textdriver, dado que cada archivo es una tabla.  
  
## <a name="sqldbmsver"></a>SQL_DBMS_VER  
  
|ISAM|Versión|Formato de números de versión|  
|----------|-------------|-------------------------------|  
|Texto|1,0|01.00.0000|  
  
## <a name="sqlcatalogusage"></a>SQL_CATALOG_USAGE  
 SQL_QU_DML_STATEMENTS &AMP;#124; SQL_QU_TABLE_DEFINITION  
  
## <a name="sqltimedatefunctions"></a>SQL_TIMEDATE_FUNCTIONS  
 SQL_FN_TD_CURDATE &AMP;#124; SQL_FN_TD_CURTIME &AMP;#124; SQL_FN_TD_DAYOFMONTH &AMP;#124; SQL_FN_TD_DAYOFWEEK &AMP;#124; SQL_FN_TD_DAYOFYEAR &AMP;#124; SQL_FN_TD_HOUR &AMP;#124; SQL_FN_TD_MINUTE &AMP;#124; SQL_FN_TD_MONTH &AMP;#124; SQL_FN_TD_NOW &AMP;#124; SQL_FN_TD_SECOND &AMP;#124; SQL_FN_TD_WEEK &AMP;#124; SQL_FN_TD_YEAR
