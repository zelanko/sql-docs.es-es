---
title: Obtención de asas de descriptores de la mano de la obtuviera de los Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c17b693080c2727d2ee788b74f247d86d7a3cb27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302350"
---
# <a name="obtaining-descriptor-handles"></a>Obtener el Descriptor controla
Una aplicación obtiene el identificador de cualquier descriptor asignado explícitamente como argumento de salida de la llamada a **SQLAllocHandle**. El identificador de un descriptor asignado implícitamente se obtiene llamando a **SQLGetStmtAttr**.
