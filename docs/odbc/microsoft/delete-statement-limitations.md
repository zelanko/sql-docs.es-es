---
title: "Limitaciones de instrucción DELETE | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cce6402f913348dd3b9aa3d116b7ceffb5a55ea4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="delete-statement-limitations"></a>ELIMINAR las limitaciones de instrucción
La instrucción DELETE no se admite para el controlador de Microsoft Excel o texto. Tenga en cuenta que la instrucción INSERT es compatible con el controlador de texto.  
  
 El controlador dBASE no admite el empaquetado de una tabla para quitar valores de "eliminar".  
  
 Para que el controlador de Paradox eliminar una fila de una tabla, la tabla debe tener un índice único (clave principal Paradox).
