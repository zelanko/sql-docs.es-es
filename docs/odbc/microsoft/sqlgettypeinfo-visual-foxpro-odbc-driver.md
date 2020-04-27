---
title: SQLGetTypeInfo (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetTypeInfo function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 5f25e20b-a4ef-42da-aeb6-00e0510fb1cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 23db0350f0f7271f85e2bc5c6a9e6c8767443a85
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "81299525"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel 1  
  
 Devuelve información sobre los tipos de datos admitidos por un origen de datos. El controlador devuelve la información en un conjunto de resultados de SQL. En la tabla siguiente se enumeran los tipos de datos de ODBC y el tipo de datos de Visual FoxPro correspondiente.  
  
|Tipo de ODBC|Tipo de Visual FoxPro|  
|---------------|------------------------|  
|SQL_BIGINT|No compatible. No hay ningún tipo de Visual FoxPro de 64 bits.|  
|SQL_BIT|Lógicos|  
|SQL_CHAR|Carácter|  
|SQL_DATE|Fecha|  
|SQL_DECIMAL|Numeric|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Entero|  
|SQL_LONGVARBINARY|Memorando (binario)|  
|SQL_LONGVARCHAR|Memorándum|  
|SQL_NUMERIC|Numeric *, Currency, Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Entero|  
|SQL_TIME|No compatible. No hay ningún tipo de *hora* de Visual FoxPro.|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Entero|  
|SQL_VARBINARY|Memorando (binario) *, general|  
|SQL_VARCHAR|Carácter|  
  
 * Tipo predeterminado  
  
 Para obtener más información sobre los tipos de datos de Visual FoxPro, vea [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md). Para obtener más información sobre esta función, vea [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) en la *Referencia del programador de ODBC*.
