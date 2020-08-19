---
description: Varios hstmts (controlador de Paradox)
title: Varios hstmts (controlador de Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- multiple hstmts [ODBC]
- Paradox driver [ODBC], multiple hstmts
ms.assetid: 66aecd94-092d-43d4-9583-74f5e2990eac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 687b87f07142ad23f6faf7155ae974a6d93deab4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449407"
---
# <a name="multiple-hstmts-paradox-driver"></a>Varios hstmts (controlador de Paradox)
Cuando se utiliza el controlador ODBC de Paradox, si desea utilizar más de un *hstmt* para ejecutar consultas en una tabla, la tabla debe tener un índice único (clave principal de Paradox).
