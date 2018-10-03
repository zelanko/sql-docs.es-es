---
title: 'Jet: Fecha, hora y marca de tiempo literales | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2325cd7e4a10e91f351aa2107c64c0978b843fa6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825843"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Fecha, hora y marca de tiempo literales
Para obtener la máxima interoperatividad, las aplicaciones deben pasar literales de fecha en el formato canónico de ODBC con la sintaxis de la cláusula de escape:  
  
-   Para los literales de fecha, {d. '*valor*"}, donde *valo*e tiene el formato"aaaa-mm-dd"  
  
-   Para los literales de hora, {t '*valor*"}, donde *valo*e tiene el formato"hh"  
  
 Marca de tiempo literales {ts'*valor*'}, donde *valo*e tiene el formato "aaaa-mm-dd hh: mm: [. f...]".
