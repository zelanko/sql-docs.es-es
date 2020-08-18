---
description: QUITAR las limitaciones de declaración de tabla
title: Limitaciones de la instrucción DROP TABLE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, DROP TABLE statement limitations
- DROP TABLE statement limitations [ODBC]
ms.assetid: 0a1c80f5-c9f2-4655-9bfd-0131b2f015a9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9d56e53d8a17c15736e9423e5920c81f864e2973
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412561"
---
# <a name="drop-table-statement-limitations"></a>QUITAR las limitaciones de declaración de tabla
Cuando se utiliza el controlador Microsoft Excel 5,0, 7,0 o 97, la instrucción DROP TABLE borra la hoja de cálculo, pero no elimina el nombre de la hoja de cálculo. Dado que el nombre de la hoja de cálculo todavía existe en el libro, no se puede crear otra hoja de cálculo con el mismo nombre.
