---
title: Funciones de cadena (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC string functions [ODBC]
- string functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], string functions
- FoxPro ODBC driver [ODBC], string functions
ms.assetid: 1974fd26-ef0d-45d5-860b-298917c8e9c3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db1fbaffbee0f74625f4a11cad3b961f194e3829
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948774"
---
# <a name="string-functions-visual-foxpro-odbc-driver"></a>Funciones de cadena (el controlador ODBC de Visual FoxPro)
En la tabla siguiente se enumeran las funciones de manipulación de cadenas ODBC compatibles con el controlador ODBC de Visual FoxPro; Cuando la gramática de Visual FoxPro para la misma función difiere de la sintaxis de ODBC, se muestra el equivalente de Visual FoxPro.  
  
|Gramática de ODBC|Gramática de Visual FoxPro|  
|------------------|---------------------------|  
|ASCII *(string_exp)*|ASC *(string_exp)*|  
|CHAR *(código)*|CHR *(string_exp)*|  
|CONCAt *(string_exp1, string_exp2)*|*string_exp1 + string_exp2*|  
|DIFERENCIA *(string_exp1, string_exp2)*||  
|INSERT *(string_exp1, Inicio, longitud string_exp2)*|COSAS *(string_exp1, Inicio, longitud string_exp2)*|  
|LCASE *(string_exp)*|LOWER *(string_exp)*|  
|LEFT *(string_exp, Count)*||  
|LONGITUD *(string_exp)*|LEN *(string_exp)*|  
|LTRIM *(string_exp)*||  
|REPEAT *(string_exp, Count)*|REPLICAte *(string_exp, Count)*|  
|Replace *(string_exp1, string_exp2, string_exp3)*|STRTRAN *(string_exp1, string_exp2, string_exp3)*|  
|RIGHT *(string_exp, Count)*||  
|RTRIM *(string_exp)*||  
|SOUNDEX *(string_exp)*||  
|ESPACIO *(recuento)*||  
|Substring *(string_exp, Inicio, longitud)*|SUBSTR *(string_exp, Inicio, longitud)*|  
|UCASE *(string_exp)*|UPPER *(string_exp)*|
