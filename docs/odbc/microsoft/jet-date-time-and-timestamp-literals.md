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
ms.openlocfilehash: 1bb7f0fb02049b6d2f1897c4f495035aee2858f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085492"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Fecha, hora y marca de tiempo literales
Para obtener la máxima interoperatividad, las aplicaciones deben pasar literales de fecha en el formato canónico de ODBC con la sintaxis de la cláusula de escape:  
  
-   Para los literales de fecha, {d. '*valor*"}, donde *valo*e tiene el formato"aaaa-mm-dd"  
  
-   Para los literales de hora, {t '*valor*"}, donde *valo*e tiene el formato"hh"  
  
 Marca de tiempo literales {ts'*valor*'}, donde *valo*e tiene el formato "aaaa-mm-dd hh: mm: [. f...]".
