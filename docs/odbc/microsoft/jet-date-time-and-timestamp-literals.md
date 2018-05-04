---
title: 'Jet: Fecha, hora y marca de tiempo literales | Documentos de Microsoft'
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
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc36c46885a358e1ca453901fd72362ed1dbb32b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Fecha, hora y marca de tiempo literales
Para obtener una interoperabilidad máxima, las aplicaciones deberían pasar literales de fecha en el formato canónico de ODBC mediante la sintaxis de la cláusula de escape:  
  
-   Para los literales de fecha, {d. '*valor*'}, donde *formato de valor*e tiene el formato "aaaa-mm-dd"  
  
-   Para los literales de hora, {t '*valor*'}, donde *formato de valor*e tiene el formato "hh"  
  
 Para los literales de marca de tiempo de {ts'*valor*'}, donde *formato de valor*e tiene el formato "aaaa-mm-dd hh [. f...]".
