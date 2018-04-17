---
title: Comparar marcadores | Documentos de Microsoft
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
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 44561e4386353ef1efaf3dd41e5a24b93941963d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="comparing-bookmarks"></a>Comparación de marcadores
Dado que los marcadores son comparables de bytes, que se puedan comparar igualdad o desigualdad. Para ello, una aplicación trata cada marcador como una matriz de bytes y compara dos marcadores byte a byte. Dado que se garantiza que los marcadores ser distintos solo dentro de un conjunto de resultados, no tiene sentido para comparar los marcadores que se obtuvieron de distintos conjuntos de resultados.
