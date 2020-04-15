---
title: Limitaciones de la declaración UPDATE (UPDATE Statement Limitations) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8ddf19c0b672901b2e778833f8bf624996d4ced3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307626"
---
# <a name="update-statement-limitations"></a>Limitaciones de la instrucción de actualización
Para que el controlador Paradox actualice una tabla, la tabla debe tener un índice único (clave principal de Paradox). Cuando se utiliza el controlador Paradox sin implementar El motor de base de datos de Borland, no es posible actualizar una tabla de Paradox.  
  
 No es compatible con el controlador de texto.  
  
 Cuando se usa el controlador de Microsoft Excel, es posible actualizar valores, pero no se puede eliminar una fila de una tabla basada en una hoja de cálculo de Microsoft Excel. Como resultado, la instrucción UPDATE no se considera admitida oficialmente por el controlador de Microsoft Excel. Solo se considera compatible la instrucción INSERT.
