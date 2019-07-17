---
title: Tipos de datos admitidos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f5ec0f3943fd52540f094a23e9b3f9f3886e1371
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114076"
---
# <a name="supported-data-types"></a>Tipos de datos admitidos
Los tipos de datos compatibles con los DBMS varían considerablemente. Una aplicación puede determinar los nombres y las características de los tipos de datos admitidos por una llamada a **SQLGetTypeInfo**. Debido a la gran variación en los nombres de tipo de datos, la aplicación debe utilizar los nombres de tipo de datos devueltos por **SQLGetTypeInfo** en **CREATE TABLE** instrucciones. Para obtener más información, consulte [tipos de datos de ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
