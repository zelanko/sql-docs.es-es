---
title: Limitaciones de la instrucción de actualización | Documentos de Microsoft
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
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbb1e6cbf0660f7b016391d5881b77d7e89e1f81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="update-statement-limitations"></a>Limitaciones de la instrucción de actualización
Para que el controlador de Paradox actualizar una tabla, la tabla debe tener un índice único (clave principal Paradox). Cuando se usa el controlador de Paradox sin necesidad de implementar el motor de base de datos de Borland, no es posible actualizar una tabla de Paradox.  
  
 No se admite el controlador de texto.  
  
 Cuando se utiliza el controlador de Microsoft Excel, es posible actualizar los valores, pero no se puede eliminar una fila de una tabla basada en una hoja de cálculo de Microsoft Excel. Como resultado, la instrucción UPDATE no se considera compatible oficialmente con el controlador de Microsoft Excel. Solo la instrucción INSERT se considera compatible.
