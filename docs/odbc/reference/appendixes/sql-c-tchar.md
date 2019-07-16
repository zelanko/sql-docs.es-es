---
title: SQL_C_TCHAR | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 68a03de54a8a5f63a994578d64c6bce5a1279138
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057037"
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
El identificador del tipo SQL_C_TCHAR no identificar realmente un tipo de datos; es una macro que existe en el archivo de encabezado para la conversión de Unicode. Se sustituye por SQL_C_CHAR o SQL_C_WCHAR dependiendo del valor de UNICODE **#define**. Es útil para una aplicación de transferencia de datos de caracteres que se compilan como un ANSI y una aplicación Unicode.
