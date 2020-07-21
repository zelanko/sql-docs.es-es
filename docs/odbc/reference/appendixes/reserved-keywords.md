---
title: Palabras clave reservadas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC function call reserved words [ODBC]
- reserved keywords [ODBC]
ms.assetid: 8eeede59-a828-44bf-866c-1ca9a77a2c5e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ed8056d6c9645a211f1413a1b280426925dd538e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307996"
---
# <a name="reserved-keywords"></a>Palabras clave reservadas
Las siguientes palabras están reservadas para su uso en llamadas a funciones de ODBC. Estas palabras no restringen la gramática de SQL mínima; sin embargo, para garantizar la compatibilidad con los controladores que admiten la gramática básica de SQL, las aplicaciones deben evitar el uso de cualquiera de estas palabras clave. El valor de #**define** SQL_ODBC_KEYWORDS contiene una lista separada por comas de estas palabras clave.  
  
|||  
|-|-|  
|ABSOLUTE|IS|  
|ACTION|ISOLATION|  
|ADA|JOIN|  
|ADD|KEY|  
|ALL|LANGUAGE|  
|ALLOCATE|LAST|  
|ALTER|LEADING|  
|y|LEFT|  
|ANY|LEVEL|  
|ARE|LIKE|  
|AS|LOCAL|  
|ASC|LOWER|  
|ASSERTION|MATCH|  
|AT|MÁX|  
|AUTHORIZATION|MÍN|  
|MEDIA|MINUTE|  
|BEGIN|MODULE|  
|BETWEEN|MONTH|  
|BIT|NAMES|  
|BIT_LENGTH|NATIONAL|  
|BOTH|NATURAL|  
|BY|NCHAR|  
|CASCADE|NEXT|  
|CASCADED|No|  
|CASE|Ninguno|  
|CAST|NOT|  
|CATALOG|NULL|  
|CHAR|NULLIF|  
|CHAR_LENGTH|NUMERIC|  
|CHARACTER|OCTET_LENGTH|  
|CHARACTER_LENGTH|OF|  
|CHECK|ACTIVAR|  
|CLOSE|ONLY|  
|COALESCE|OPEN|  
|COLLATE|OPTION|  
|COLLATION|O BIEN|  
|COLUMN|ORDER|  
|COMMIT|OUTER|  
|CONNECT|OUTPUT|  
|CONNECTION|OVERLAPS|  
|CONSTRAINT|PAD|  
|CONSTRAINTS|PARTIAL|  
|CONTINUE|PASCAL|  
|CONVERT|POSITION|  
|CORRESPONDING|PRECISION|  
|COUNT|PREPARE|  
|CREATE|PRESERVE|  
|CROSS|PRIMARY|  
|CURRENT|PRIOR|  
|CURRENT_DATE|PRIVILEGES|  
|CURRENT_TIME|PROCEDURE|  
|CURRENT_TIMESTAMP|PUBLIC|  
|CURRENT_USER|READ|  
|CURSOR|real|  
|DATE|REFERENCES|  
|DAY|RELATIVE|  
|DEALLOCATE|RESTRICT|  
|DEC|REVOKE|  
|DECIMAL|RIGHT|  
|DECLARE|ROLLBACK|  
|DEFAULT|ROWS|  
|DEFERRABLE|SCHEMA|  
|DEFERRED|SCROLL|  
|Delete|SECOND|  
|DESC|SECTION|  
|DESCRIBE|SELECT|  
|DESCRIPTOR|SESSION|  
|DIAGNOSTICS|SESSION_USER|  
|DISCONNECT|SET|  
|DISTINCT|SIZE|  
|DOMAIN|SMALLINT|  
|DOUBLE|SOME|  
|DROP|SPACE|  
|ELSE|SQL|  
|END|SQLCA|  
|END-EXEC|SQLCODE|  
|ESCAPE|SQLERROR|  
|EXCEPT|SQLSTATE|  
|EXCEPTION|SQLWARNING|  
|EXEC|SUBSTRING|  
|Ejecute|SUM|  
|EXISTS|SYSTEM_USER|  
|EXTERNAL|TABLE|  
|EXTRACT|TEMPORARY|  
|FALSE|THEN|  
|FETCH|TIME|  
|FIRST|timestamp|  
|FLOAT|TIMEZONE_HOUR|  
|FOR|TIMEZONE_MINUTE|  
|FOREIGN|TO|  
|FORTRAN|TRAILING|  
|FOUND|TRANSACTION|  
|FROM|TRANSLATE|  
|FULL|TRANSLATION|  
|GET|TRIM|  
|GLOBAL|TRUE|  
|GO|UNION|  
|GOTO|UNIQUE|  
|GRANT|DESCONOCIDO|  
|GROUP|UPDATE|  
|HAVING|UPPER|  
|HOUR|USAGE|  
|IDENTITY|USER|  
|IMMEDIATE|USING|  
|IN|VALOR|  
|INCLUDE|VALUES|  
|INDEX|VARCHAR|  
|INDICATOR|VARYING|  
|INITIALLY|VIEW|  
|INNER|WHEN|  
|INPUT|WHENEVER|  
|INSENSITIVE|WHERE|  
|INSERT|WITH|  
|INT|WORK|  
|INTEGER|WRITE|  
|INTERSECT|YEAR|  
|INTERVAL|ZONE|  
|INTO||
