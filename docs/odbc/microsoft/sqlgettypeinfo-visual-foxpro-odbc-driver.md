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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f29be5e03a6cc9c1c91809db2b8ec7c686e90f11
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67898626"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel 1  
  
 Devuelve información sobre los tipos de datos admitidos por un origen de datos. El controlador devuelve la información en un conjunto de resultados de SQL. En la tabla siguiente se enumeran los tipos de datos de ODBC y el tipo de datos de Visual FoxPro correspondiente.  
  
|Tipo ODBC|Tipo de Visual FoxPro|  
|---------------|------------------------|  
|SQL_BIGINT|No compatible. No hay ningún tipo de Visual FoxPro de 64 bits.|  
|SQL_BIT|Lógicos|  
|SQL_CHAR|Character|  
|SQL_DATE|Date|  
|SQL_DECIMAL|Numeric|  
|SQL_DOUBLE|DOUBLE|  
|SQL_FLOAT|DOUBLE|  
|SQL_INTEGER|Entero|  
|SQL_LONGVARBINARY|Memorando (binario)|  
|SQL_LONGVARCHAR|Memorándum|  
|SQL_NUMERIC|Numeric *, Currency, Float|  
|SQL_REAL|DOUBLE|  
|SQL_SMALLINT|Entero|  
|SQL_TIME|No compatible. No hay ningún tipo de *hora* de Visual FoxPro.|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Entero|  
|SQL_VARBINARY|Memorando (binario) *, general|  
|SQL_VARCHAR|Character|  
  
 * Tipo predeterminado  
  
 Para obtener más información sobre los tipos de datos de Visual FoxPro, vea [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md). Para obtener más información sobre esta función, vea [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) en la *Referencia del programador de ODBC*.
