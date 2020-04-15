---
title: Tipos de datos admitidos ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d19cde2d531819a60229dd7a780181571e169503
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307786"
---
# <a name="supported-data-types"></a>Tipos de datos admitidos
Los tipos de datos admitidos por LOS DBMS varían considerablemente. Una aplicación puede determinar los nombres y características de los tipos de datos admitidos llamando a **SQLGetTypeInfo**. Debido a la amplia variación en los nombres de tipo de datos, la aplicación debe usar los nombres de tipo de datos devueltos por **SQLGetTypeInfo** en **CREATE TABLE** instrucciones. Para obtener más información, vea [Tipos de datos en ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
