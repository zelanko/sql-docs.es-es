---
title: 'Jet: Fecha, Hora y Literales de marca de tiempo ? Microsoft Docs'
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
ms.openlocfilehash: 372b7c1dab1ad8ff000fb88729c3b02e05d4a21c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299944"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Fecha, hora y marca de tiempo literales
Para una interoperabilidad máxima, las aplicaciones deben pasar literales de fecha en el formato canónico ODBC mediante la sintaxis de cláusula de escape:  
  
-   En el caso de los literales de fecha, el*valor*de la fecha , donde *valu*e tiene la forma "aaaa-mm-dd"  
  
-   Para los literales de tiempo, el *valu**valor*de la versión "hh:mm:ss" es "hh:mm:ss"  
  
 En el caso de los literales de marca de tiempo , el*valor*'', donde *valu*e tiene la forma "aaaa-mm-dd hh:mm:ss[.f...]".
