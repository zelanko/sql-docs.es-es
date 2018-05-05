---
title: Número de versión | Documentos de Microsoft
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
- version number supported [ODBC]
- interoperability [ODBC], version number supported
ms.assetid: 6eccacdf-b837-4b66-bd48-ba31771acecb
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05629fd8d944ed62325a3af5a18d8431c49e1aa2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="version-number"></a>Número de versión
Hay varias versiones de ODBC, cada una con diferentes características. Una aplicación determina que admiten la versión de ODBC el Administrador de controladores y un controlador específico mediante una llamada a **SQLGetInfo** con las opciones SQL_ODBC_VER y SQL_DRIVER_ODBC_VER.
