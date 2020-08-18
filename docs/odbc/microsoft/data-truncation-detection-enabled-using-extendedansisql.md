---
description: Habilita la detección de truncamiento de datos utilizando ExtendedAnsiSQL
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
ms.openlocfilehash: 26965093caecbc11e94ef738ba6b8ff757b43258
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412896"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>Habilita la detección de truncamiento de datos utilizando ExtendedAnsiSQL
Cuando la marca ExtendedAnsiSQL está activada y la aplicación está insertando datos en una columna CHAR o binary y los datos se truncan, se detectará el truncamiento. Cuando se desactiva la marca ExtendedAnsiSQL, los datos se truncan sin previo aviso, como en las versiones anteriores de los controladores de base de datos de escritorio ODBC.
