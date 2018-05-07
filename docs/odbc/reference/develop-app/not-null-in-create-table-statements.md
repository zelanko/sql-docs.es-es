---
title: NO es NULL en las instrucciones de CREATE TABLE | Documentos de Microsoft
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
- not null [ODBC]
- interoperability [ODBC], not null
ms.assetid: 3fb69943-f0c9-4ed2-aa42-20440e37e49d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5b1c2d2a96e12e09341d4bf34811bc7bcb6694e3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="not-null-in-create-table-statements"></a>NOT NULL en las instrucciones de CREATE TABLE
Algunas bases de datos y especialmente escritorio, no admiten la **NOT NULL** restricción de columna en **CREATE TABLE** instrucciones. Para obtener más información, vea la opción SQL_NON_NULLABLE_COLUMNS en la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.
