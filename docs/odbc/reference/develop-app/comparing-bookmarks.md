---
title: Comparar marcadores | Documentos de Microsoft
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
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 7ebcf375311af498dbb4c777707b7febcddb05a3
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="comparing-bookmarks"></a>Comparación de marcadores
Dado que los marcadores son comparables de bytes, que se puedan comparar igualdad o desigualdad. Para ello, una aplicación trata cada marcador como una matriz de bytes y compara dos marcadores byte a byte. Dado que se garantiza que los marcadores ser distintos solo dentro de un conjunto de resultados, no tiene sentido para comparar los marcadores que se obtuvieron de distintos conjuntos de resultados.

