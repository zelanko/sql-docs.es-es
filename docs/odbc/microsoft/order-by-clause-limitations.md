---
title: ORDEN por cláusula limitaciones | Documentos de Microsoft
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
- ODBC SQL grammar, ORDER BY clause limitations
- ORDER BY clause limitations [ODBC]
ms.assetid: fd4ddc7c-9c7e-4a0c-a781-e5427dfb2e18
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7eb96840ec20338b8d7739b2332d63bea25c765d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="order-by-clause-limitations"></a>ORDEN por cláusula limitaciones
Si una instrucción SELECT contiene una cláusula GROUP BY y una cláusula ORDER BY, la cláusula ORDER BY puede contener solo una columna del conjunto de resultados o una expresión en la cláusula GROUP BY.
