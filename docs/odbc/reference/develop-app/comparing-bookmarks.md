---
title: Comparación de marcadores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- comparing bookmarks [ODBC]
- bookmarks [ODBC]
ms.assetid: ea347635-fbe3-41c1-b537-4048b7c0f7da
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 690acf80bfabdc04d5f70b780e41943337c18cb9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026612"
---
# <a name="comparing-bookmarks"></a>Comparación de marcadores
Dado que los marcadores son comparables de bytes, que se puedan comparar igualdad o desigualdad. Para ello, una aplicación trata cada marcador como una matriz de bytes y compara los dos marcadores byte a byte. Dado que los marcadores se garantiza que sean distintos solo dentro de un conjunto de resultados, no tiene sentido para comparar los marcadores que se obtuvieron de distintos conjuntos de resultados.
