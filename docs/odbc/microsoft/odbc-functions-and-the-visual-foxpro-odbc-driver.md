---
description: Funciones ODBC y el controlador ODBC de Visual FoxPro
title: Funciones ODBC y el controlador ODBC de Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC level 2 API functions [ODBC]
- ODBC level 1 API functions [ODBC]
- functions [ODBC], API
- ODBC API functions [ODBC]
- level 1 API functions [ODBC]
- API functions [ODBC]
- core level API functions [ODBC]
- level 2 API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 512f9cee-ffad-439b-b612-b49c34c32658
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 017e66c137f6c0921f3a382c0832598c9415c9e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340741"
---
# <a name="odbc-functions-and-the-visual-foxpro-odbc-driver"></a>Funciones ODBC y el controlador ODBC de Visual FoxPro
En los temas de esta sección se proporciona un breve resumen de las funciones de la API de ODBC y cualquier detalle específico de Visual FoxPro.  
  
> [!NOTE]  
>  Para obtener información general sobre las funciones de ODBC, vea referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md) en "Guía del programador de ODBC".  
  
 Las funciones de la API de ODBC se han dividido en tres categorías principales: funciones de API de nivel básico, funciones de API de nivel 1 y funciones de API de nivel 2.  
  
> [!NOTE]  
>  Algunas de las funciones se comportan de manera diferente dependiendo de si el origen de datos se define como una conexión a un directorio de [tablas libres](../../odbc/microsoft/visual-foxpro-terminology.md) (archivos. dbf) o a una [base](../../odbc/microsoft/visual-foxpro-terminology.md) de datos de Visual FoxPro (archivo. DBC). Ciertas operaciones solo se admiten para las conexiones de base de datos.  
  
## <a name="core-level-api-support"></a>Compatibilidad con API de nivel básico  
 En la tabla siguiente se enumeran las funciones de API de nivel básico de ODBC. Todas estas funciones son compatibles con el controlador ODBC de Visual FoxPro.  

:::row:::
    :::column:::
        [SQLAllocConnect](../../odbc/microsoft/sqlallocconnect-visual-foxpro-odbc-driver.md)  
        [SQLAllocEnv](../../odbc/microsoft/sqlallocenv-visual-foxpro-odbc-driver.md)  
        [SQLAllocStmt](../../odbc/microsoft/sqlallocstmt-visual-foxpro-odbc-driver.md)  
        [SQLBindCol](../../odbc/microsoft/sqlbindcol-visual-foxpro-odbc-driver.md)  
        [SQLCancel](../../odbc/microsoft/sqlcancel-visual-foxpro-odbc-driver.md)  
        [SQLColAttributes](../../odbc/microsoft/sqlcolattributes-visual-foxpro-odbc-driver.md)  
        [SQLConnect](../../odbc/microsoft/sqlconnect-visual-foxpro-odbc-driver.md)  
        [SQLDescribeCol](../../odbc/microsoft/sqldescribecol-visual-foxpro-odbc-driver.md)  
        [SQLDisconnect](../../odbc/microsoft/sqldisconnect-visual-foxpro-odbc-driver.md)  
        [SQLError](../../odbc/microsoft/sqlerror-visual-foxpro-odbc-driver.md)  
        [SQLExecDirect](../../odbc/microsoft/sqlexecdirect-visual-foxpro-odbc-driver.md)  
    :::column-end:::
    :::column:::
        [SQLExecute](../../odbc/microsoft/sqlexecute-visual-foxpro-odbc-driver.md)  
        [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md)  
        [SQLFreeConnect](../../odbc/microsoft/sqlfreeconnect-visual-foxpro-odbc-driver.md)  
        [SQLFreeEnv](../../odbc/microsoft/sqlfreeenv-visual-foxpro-odbc-driver.md)  
        [SQLFreeStmt](../../odbc/microsoft/sqlfreestmt-visual-foxpro-odbc-driver.md)  
        [SQLGetCursorName](../../odbc/microsoft/sqlgetcursorname-visual-foxpro-odbc-driver.md)  
        [SQLNumResultCols](../../odbc/microsoft/sqlnumresultcols-visual-foxpro-odbc-driver.md)  
        [SQLPrepare](../../odbc/microsoft/sqlprepare-visual-foxpro-odbc-driver.md)  
        [SQLRowCount](../../odbc/microsoft/sql-row-count-visual-foxpro-odbc-driver.md)  
        [SQLSetCursorName](../../odbc/microsoft/sqlsetcursorname-visual-foxpro-odbc-driver.md)  
        [SQLTransact](../../odbc/microsoft/sqltransact-visual-foxpro-odbc-driver.md)  
    :::column-end:::
:::row-end:::

## <a name="level-1-api-support"></a>Compatibilidad con la API de nivel 1  
 En la tabla siguiente se enumeran las funciones de la API de ODBC de nivel 1. Todas estas funciones son totalmente compatibles con el controlador ODBC de Visual FoxPro.  

:::row:::
    :::column:::
        [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md)  
        [SQLColumns](../../odbc/microsoft/sqlcolumns-visual-foxpro-odbc-driver.md)  
        [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md)  
        [SQLGetConnectOption](../../odbc/microsoft/sqlgetconnectoption-visual-foxpro-odbc-driver.md)  
        [SQLGetData](../../odbc/microsoft/sqlgetdata-visual-foxpro-odbc-driver.md)  
        [SQLGetFunctions](../../odbc/microsoft/sqlgetfunctions-visual-foxpro-odbc-driver.md)  
        [SQLGetInfo](../../odbc/microsoft/sqlgetinfo-visual-foxpro-odbc-driver.md)  
        [SQLGetStmtOption](../../odbc/microsoft/sqlgetstmtoption-visual-foxpro-odbc-driver.md)  
    :::column-end:::
    :::column:::
        [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md)  
        [SQLParamData](../../odbc/microsoft/sqlparamdata-visual-foxpro-odbc-driver.md)  
        [SQLPutData](../../odbc/microsoft/sqlputdata-visual-foxpro-odbc-driver.md)  
        [SQLSetConnectOption](../../odbc/microsoft/sqlsetconnectoption-visual-foxpro-odbc-driver.md)  
        [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md)  
        [SQLSpecialColumns](../../odbc/microsoft/sqlspecialcolumns-visual-foxpro-odbc-driver.md)  
        [SQLStatistics](../../odbc/microsoft/sqlstatistics-visual-foxpro-odbc-driver.md)  
        [SQLTables](../../odbc/microsoft/sqltables-visual-foxpro-odbc-driver.md)  
    :::column-end:::
:::row-end:::

## <a name="level-2-api-support"></a>Compatibilidad con la API de nivel 2  
 Las siguientes funciones de API de nivel 2 de ODBC se admiten total o parcialmente:  
  
-   [SQLDataSources](../../odbc/microsoft/sqldatasources-visual-foxpro-odbc-driver.md)  
  
-   [SQLDrivers](../../odbc/microsoft/sqldrivers-visual-foxpro-odbc-driver.md)  
  
-   [SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md)  
  
-   [SQLMoreResults](../../odbc/microsoft/sqlmoreresults-visual-foxpro-odbc-driver.md)  
  
-   [SQLNumParams](../../odbc/microsoft/sqlnumparams-visual-foxpro-odbc-driver.md)  
  
-   [SQLParamOptions](../../odbc/microsoft/sqlparamoptions-visual-foxpro-odbc-driver.md)  
  
-   [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetPos](../../odbc/microsoft/sqlsetpos-visual-foxpro-odbc-driver.md)  
  
-   [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) (compatibilidad parcial)  
  
 No se admiten las siguientes funciones de API de nivel 2:  
  
-   SQLBrowseConnect  
  
-   SQLColumnPrivileges  
  
-   SQLDescribeParam  
  
-   SQLForeignKeys  
  
-   SQLNativeSql  
  
-   SQLProcedureColumns  
  
-   SQLProcedures  
  
-   SQLTablePrivileges
