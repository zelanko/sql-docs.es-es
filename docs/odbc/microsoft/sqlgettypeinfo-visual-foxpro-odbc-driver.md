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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898626"
---
# <a name="sqlgettypeinfo-visual-foxpro-odbc-driver"></a>SQLGetTypeInfo (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Completo  
  
 Conformidad de la API de ODBC: Nivel 1  
  
 Devuelve información sobre los tipos de datos admitidos por un origen de datos. El controlador devuelve la información en un conjunto de resultados SQL. En la tabla siguiente se enumera los tipos de datos ODBC y el tipo de datos de Visual FoxPro correspondiente.  
  
|Tipo de ODBC|Tipo de objeto Visual FoxPro|  
|---------------|------------------------|  
|SQL_BIGINT|No compatible. No hay ningún tipo de Visual FoxPro de 64 bits.|  
|SQL_BIT|Lógico|  
|SQL_CHAR|Carácter|  
|SQL_DATE|Date|  
|SQL_DECIMAL|Numeric|  
|SQL_DOUBLE|Double|  
|SQL_FLOAT|Double|  
|SQL_INTEGER|Entero|  
|SQL_LONGVARBINARY|Memorando (binario)|  
|SQL_LONGVARCHAR|Memorándum|  
|SQL_NUMERIC|*, Moneda, numéricos Float|  
|SQL_REAL|Double|  
|SQL_SMALLINT|Entero|  
|SQL_TIME|No compatible. No hay ningún Visual FoxPro *tiempo* tipo.|  
|SQL_TIMESTAMP|DateTime|  
|SQL_TINYINT|Entero|  
|SQL_VARBINARY|Memorando (binario) *, General|  
|SQL_VARCHAR|Carácter|  
  
 \* Tipo predeterminado  
  
 Para obtener más información acerca de los tipos de datos de Visual FoxPro, consulte [CREATE TABLE](../../odbc/microsoft/create-table-sql-command.md). Para obtener más información acerca de esta función, vea [SQLGetTypeInfo](../../odbc/reference/syntax/sqlgettypeinfo-function.md) en el *referencia del programador de ODBC*.
