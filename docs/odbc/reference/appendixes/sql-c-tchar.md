---
description: SQL_C_TCHAR
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6fc7ff6e6334d49acc4e230b5fb12feb3f85556e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483178"
---
# <a name="sql_c_tchar"></a>SQL_C_TCHAR
En realidad, el identificador de tipo SQL_C_TCHAR no identifica un tipo de datos. se trata de una macro que existe en el archivo de encabezado para la conversión Unicode. Se reemplaza por SQL_C_CHAR o SQL_C_WCHAR en función de la configuración de la **#define**Unicode. Resulta útil para una aplicación que transfiera datos de caracteres compilados como una aplicación ANSI y Unicode.
