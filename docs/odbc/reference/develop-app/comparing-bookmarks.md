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
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792703"
---
# <a name="comparing-bookmarks"></a>Comparación de marcadores
Dado que los marcadores son comparables de bytes, que se puedan comparar igualdad o desigualdad. Para ello, una aplicación trata cada marcador como una matriz de bytes y compara los dos marcadores byte a byte. Dado que los marcadores se garantiza que sean distintos solo dentro de un conjunto de resultados, no tiene sentido para comparar los marcadores que se obtuvieron de distintos conjuntos de resultados.
