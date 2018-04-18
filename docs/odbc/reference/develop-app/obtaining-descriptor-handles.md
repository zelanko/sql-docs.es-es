---
title: Obtener el Descriptor controla | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f66fb64b8d54e2b620779e6548e9ff4a965d31ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="obtaining-descriptor-handles"></a>Obtener el Descriptor controla
Una aplicación obtiene el identificador de cualquier descriptor asignado explícitamente como un argumento de salida de la llamada a **SQLAllocHandle**. Se obtiene el identificador de un descriptor asignado implícitamente mediante una llamada a **SQLGetStmtAttr**.
