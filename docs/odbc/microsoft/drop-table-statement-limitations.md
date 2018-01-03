---
title: "Limitaciones de instrucción de colocar tabla | Documentos de Microsoft"
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
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b7dacdba7278218e259173adf7bb19368b4bbc85
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="drop-table-statement-limitations"></a>QUITAR las limitaciones de declaración de tabla
Cuando se usa el controlador de Microsoft Excel 5.0, 7.0 ó 97, la instrucción DROP TABLE borra la hoja de cálculo, pero no elimina el nombre de la hoja de cálculo. Dado que el nombre de la hoja de cálculo todavía existe en el libro, otra hoja de cálculo no se puede crear con el mismo nombre.
