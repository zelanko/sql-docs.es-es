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
manager: craigg
ms.openlocfilehash: 2a8848bad9d27dfd9318b725b77203706d3dfd5a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753263"
---
# <a name="supported-data-types"></a>Tipos de datos admitidos
Los tipos de datos compatibles con los DBMS varían considerablemente. Una aplicación puede determinar los nombres y las características de los tipos de datos admitidos por una llamada a **SQLGetTypeInfo**. Debido a la gran variación en los nombres de tipo de datos, la aplicación debe utilizar los nombres de tipo de datos devueltos por **SQLGetTypeInfo** en **CREATE TABLE** instrucciones. Para obtener más información, consulte [tipos de datos de ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
