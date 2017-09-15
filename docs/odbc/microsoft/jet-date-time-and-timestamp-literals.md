---
title: 'Jet: Fecha, hora y marca de tiempo literales | Documentos de Microsoft'
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c1a98ca0b68198dada19e4ac81f8637798a99b95
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Fecha, hora y marca de tiempo literales
Para obtener una interoperabilidad máxima, las aplicaciones deberían pasar literales de fecha en el formato canónico de ODBC mediante la sintaxis de la cláusula de escape:  
  
-   Para los literales de fecha, {d. '*valor*'}, donde *formato de valor*e tiene el formato "aaaa-mm-dd"  
  
-   Para los literales de hora, {t '*valor*'}, donde *formato de valor*e tiene el formato "hh"  
  
 Para los literales de marca de tiempo de {ts'*valor*'}, donde *formato de valor*e tiene el formato "aaaa-mm-dd hh [. f...]".
