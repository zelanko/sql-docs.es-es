---
title: Tipos de datos admitidos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0b11c3df36ba36153f71721d9a10dee702ef745d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="supported-data-types"></a>Tipos de datos admitidos
Los tipos de datos admitidos por DBMS varían considerablemente. Una aplicación puede determinar los nombres y las características de los tipos de datos admitidos por una llamada a **SQLGetTypeInfo**. Debido a la amplia variación en los nombres de tipos de datos, la aplicación debe utilizar los nombres de tipo de datos devueltos por **SQLGetTypeInfo** en **CREATE TABLE** instrucciones. Para obtener más información, consulte [tipos de datos de ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
