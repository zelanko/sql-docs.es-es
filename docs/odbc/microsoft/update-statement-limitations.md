---
title: Limitaciones de la instrucción UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6b854cc417898c5576c60ca129c597eae280df4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826343"
---
# <a name="update-statement-limitations"></a>Limitaciones de la instrucción de actualización
Para que el controlador de Paradox actualizar una tabla, la tabla debe tener un índice único (clave principal de Paradox). Cuando se usa el controlador de Paradox sin necesidad de implementar el motor de base de datos de Borland, no es posible actualizar una tabla.  
  
 No se admite el controlador de texto.  
  
 Cuando se usa el controlador de Microsoft Excel, es posible actualizar los valores, pero no se puede eliminar una fila de una tabla basada en una hoja de cálculo de Microsoft Excel. Como resultado, la instrucción UPDATE no se considera compatible oficialmente con el controlador de Microsoft Excel. Solo la instrucción INSERT se considera compatible.
