---
title: Comparar marcadores | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c28392c0d48984b4aaf8a8df442b6a4054a7eced
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307480"
---
# <a name="comparing-bookmarks"></a>Comparación de marcadores
Dado que los marcadores son comparables en bytes, se pueden comparar la igualdad o la desigualdad. Para ello, una aplicación trata cada marcador como una matriz de bytes y compara dos marcadores byte a byte. Dado que se garantiza que los marcadores son distintos dentro de un conjunto de resultados, no tiene sentido comparar los marcadores que se obtuvieron de distintos conjuntos de resultados.
