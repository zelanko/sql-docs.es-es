---
title: Obtener el Descriptor controla | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: 936f983f-c7e9-43f3-97ea-dd4b1bbf4654
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb3d75a78a5eaa516921e561cb2d34786804d182
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="obtaining-descriptor-handles"></a>Obtener el Descriptor controla
Una aplicación obtiene el identificador de cualquier descriptor asignado explícitamente como un argumento de salida de la llamada a **SQLAllocHandle**. Se obtiene el identificador de un descriptor asignado implícitamente mediante una llamada a **SQLGetStmtAttr**.

