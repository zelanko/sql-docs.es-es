---
title: NO es NULL en las instrucciones de CREATE TABLE | Documentos de Microsoft
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
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bf0f66a1d3a5d1c7bb07ef90d25c61a99e7a7786
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="not-null-in-create-table-statements"></a>NOT NULL en las instrucciones de CREATE TABLE
Algunas bases de datos y especialmente escritorio, no admiten la **NOT NULL** restricción de columna en **CREATE TABLE** instrucciones. Para obtener más información, vea la opción SQL_NON_NULLABLE_COLUMNS en la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.
