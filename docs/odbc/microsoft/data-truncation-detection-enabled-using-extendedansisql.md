---
title: Detección de truncamiento de datos habilitada mediante ExtendedAnsiSQL | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae1aa7a8a8b9ea2c3f3054717546506e660d5270
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280706"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Habilita la detección de truncamiento de datos utilizando ExtendedAnsiSQL
Cuando la marca ExtendedAnsiSQL está activada y la aplicación está insertando datos en una columna CHAR o binary y los datos se truncan, se detectará el truncamiento. Cuando se desactiva la marca ExtendedAnsiSQL, los datos se truncan sin previo aviso, como en las versiones anteriores de los controladores de base de datos de escritorio ODBC.
