---
title: Limitaciones de la instrucción de actualización | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: 006d0f9644c9f62a6b50e2d327384ec3a9c954c1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="update-statement-limitations"></a>Limitaciones de la instrucción de actualización
Para que el controlador de Paradox actualizar una tabla, la tabla debe tener un índice único (clave principal Paradox). Cuando se usa el controlador de Paradox sin necesidad de implementar el motor de base de datos de Borland, no es posible actualizar una tabla de Paradox.  
  
 No se admite el controlador de texto.  
  
 Cuando se utiliza el controlador de Microsoft Excel, es posible actualizar los valores, pero no se puede eliminar una fila de una tabla basada en una hoja de cálculo de Microsoft Excel. Como resultado, la instrucción UPDATE no se considera compatible oficialmente con el controlador de Microsoft Excel. Solo la instrucción INSERT se considera compatible.
