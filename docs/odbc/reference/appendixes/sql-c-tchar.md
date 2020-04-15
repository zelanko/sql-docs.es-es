---
title: SQL_C_TCHAR Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 973d94b9b47371090a5f54fd3d259854ba78e9c2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304076"
---
# <a name="sql_c_tchar"></a>SQL_C_TCHAR
El identificador de tipo SQL_C_TCHAR no identifica realmente un tipo de datos; es una macro que existe dentro del archivo de encabezado para la conversión Unicode. Se sustituye por SQL_C_CHAR o SQL_C_WCHAR dependiendo de la configuración del **#define**UNICODE. Es útil para una aplicación que transfiere datos de caracteres que se compilan como una aplicación ANSI y Unicode.
