---
description: 'Jet: Fecha, hora y marca de tiempo literales'
title: 'Jet: fecha, hora y literales de marca de tiempo | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02b2a7c5c633ee891dbcd962786cb1904bfd5df8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449447"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Fecha, hora y marca de tiempo literales
Para obtener la máxima interoperabilidad, las aplicaciones deben pasar los literales de fecha en el formato canónico de ODBC mediante la sintaxis de la cláusula de escape:  
  
-   En el caso de los literales de fecha, {d '*Value*'}, donde *Valo*e tiene el formato "AAAA-MM-DD"  
  
-   En el caso de los literales de hora, {t '*Value*'}, donde *Valo*e tiene el formato "HH: mm: SS"  
  
 Para los literales de marca de tiempo {ts '*Value*'}, donde *Valo*e tiene el formato "AAAA-MM-DD HH: mm: SS [. f...]".
