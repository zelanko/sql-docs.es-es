---
title: DONDE cláusula limitaciones | Documentos de Microsoft
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
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, WHERE clause limitations
- WHERE clause limitations [ODBC]
ms.assetid: 46b54f74-e4a3-4318-87cf-8a97c38a2718
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac066f6d6728319489ff25e33b3ae479bdc7072a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="where-clause-limitations"></a>DONDE cláusula limitaciones
El número máximo de cláusulas en una cláusula WHERE es 40.  
  
 Columnas LONGVARBINARY y LONGVARCHAR pueden compararse con literales de hasta 255 caracteres de longitud, pero no se pueden comparar con parámetros.
