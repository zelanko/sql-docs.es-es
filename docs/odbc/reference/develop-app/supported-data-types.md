---
title: Tipos de datos admitidos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0820f610ca926a680acfbffc2fc2e99867860ff6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="supported-data-types"></a>Tipos de datos admitidos
Los tipos de datos admitidos por DBMS varían considerablemente. Una aplicación puede determinar los nombres y las características de los tipos de datos admitidos por una llamada a **SQLGetTypeInfo**. Debido a la amplia variación en los nombres de tipos de datos, la aplicación debe utilizar los nombres de tipo de datos devueltos por **SQLGetTypeInfo** en **CREATE TABLE** instrucciones. Para obtener más información, consulte [tipos de datos de ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
