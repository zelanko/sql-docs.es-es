---
title: SQLSetCursorName (Controladores de base de datos de escritorio) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d618a7f845a87394c2fc3c7978a7aef5716e21f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301486"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName (controladores de escritorio de la base de datos)
Dado que el controlador no admite una actualización o eliminación posicionada por la sintaxis WHERE CURRENT OF *cursorname,* **SQLSetCursorName** se admite, pero no se puede usar para las actualizaciones posicionadas. Solo se puede utilizar cuando la biblioteca de cursores está habilitada y la aplicación usa **SQLExtendedFetch**.
