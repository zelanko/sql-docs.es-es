---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a24a22a5e666421136780f3614db4df2233bc82
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801353"
---
# <a name="drop-table-statement-limitations"></a>QUITAR las limitaciones de declaración de tabla
Cuando se usa el controlador de Microsoft Excel 5.0, 7.0 ó 97, la instrucción DROP TABLE borra la hoja de cálculo, pero no elimina el nombre de la hoja de cálculo. Dado que el nombre de la hoja de cálculo sigue existiendo en el libro, no se puede crear otra hoja de cálculo con el mismo nombre.
