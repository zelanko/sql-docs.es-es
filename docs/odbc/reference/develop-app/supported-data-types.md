---
title: Tipos de datos admitidos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d76b98635cdc183f08f205374f8e7e0e66a4cb5f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="supported-data-types"></a>Tipos de datos admitidos
Los tipos de datos admitidos por DBMS varían considerablemente. Una aplicación puede determinar los nombres y las características de los tipos de datos admitidos por una llamada a **SQLGetTypeInfo**. Debido a la amplia variación en los nombres de tipos de datos, la aplicación debe utilizar los nombres de tipo de datos devueltos por **SQLGetTypeInfo** en **CREATE TABLE** instrucciones. Para obtener más información, consulte [tipos de datos de ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).

