---
description: Tipos de datos admitidos
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349636553112449485d99fed269a43069974fccf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385831"
---
# <a name="supported-data-types"></a>Tipos de datos admitidos
Los tipos de datos admitidos por DBMS varían considerablemente. Una aplicación puede determinar los nombres y las características de los tipos de datos admitidos llamando a **SQLGetTypeInfo**. Debido a la gran variación de los nombres de tipo de datos, la aplicación debe utilizar los nombres de tipo de datos devueltos por **SQLGetTypeInfo** en las instrucciones **CREATE TABLE** . Para obtener más información, vea [tipos de datos en ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
