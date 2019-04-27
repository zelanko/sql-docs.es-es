---
title: Detección de truncamiento de datos habilitada con ExtendedAnsiSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95b7d538c2ace45b42c947b56ca5a5bd5f981ec5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62744269"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Habilita la detección de truncamiento de datos utilizando ExtendedAnsiSQL
Cuando se activa la marca ExtendedAnsiSQL y la aplicación consiste en Insertar datos en un carácter o una columna binaria y se truncan los datos, se detectará el truncamiento. Cuando la marca ExtendedAnsiSQL está desactivada, los datos se truncan sin advertencia, como sucedía en versiones anteriores de los controladores de base de datos de escritorio de ODBC.
