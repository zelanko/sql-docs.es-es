---
title: Número de versión | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- version number supported [ODBC]
- interoperability [ODBC], version number supported
ms.assetid: 6eccacdf-b837-4b66-bd48-ba31771acecb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03678023990fc15d03c73501f331ecc302f6b892
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208446"
---
# <a name="version-number"></a>Número de versión
Hay varias versiones de ODBC, cada una con diferentes características. Una aplicación determina que son compatibles con la versión de ODBC el Administrador de controladores y un controlador específico mediante una llamada a **SQLGetInfo** con las opciones SQL_ODBC_VER y SQL_DRIVER_ODBC_VER.
