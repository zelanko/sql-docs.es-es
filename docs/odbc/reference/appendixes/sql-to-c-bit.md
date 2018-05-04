---
title: 'SQL con el Bit C: | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6862a94cc31bcbee1b931b18c775f03a9e1e58ef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-bit"></a>SQL con el Bit C:
El identificador para el tipo de datos SQL de ODBC de bits es:  
  
 SQL_BIT  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos SQL de bits de C de ODBC. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificador de tipo de C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* > 1<br /><br /> *BufferLength* < = 1|data<br /><br /> No definido|1<br /><br /> No definido|n/d<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|Ninguno [a]|data|Tamaño del tipo de datos C|n/d|  
|SQL_C_BIT|Ninguno [a]|data|1 [b]|n/d|  
|SQL_C_BINARY|*BufferLength* > = 1<br /><br /> *BufferLength* < 1|data<br /><br /> No definido|1<br /><br /> No definido|n/d<br /><br /> 22003|  
  
 [a] el valor de *BufferLength* se pasa por alto para esta conversión. El controlador se da por supuesto que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] es el tamaño del tipo de datos C correspondiente.  
  
 Cuando bits de datos de SQL se convierte en datos de caracteres C, los valores posibles son "0" y "1".
