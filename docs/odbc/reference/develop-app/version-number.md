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
ms.openlocfilehash: 331b60b31c49a203da5f25c4481a604132fbb0e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079552"
---
# <a name="version-number"></a>Número de versión
Hay varias versiones de ODBC, cada una con diferentes características. Una aplicación determina que son compatibles con la versión de ODBC el Administrador de controladores y un controlador específico mediante una llamada a **SQLGetInfo** con las opciones SQL_ODBC_VER y SQL_DRIVER_ODBC_VER.
