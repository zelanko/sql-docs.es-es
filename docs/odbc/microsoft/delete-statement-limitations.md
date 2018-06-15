---
title: Limitaciones de instrucción DELETE | Documentos de Microsoft
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
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caa4855c83815c8876c4674bf01de3f9c4bd4231
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32898860"
---
# <a name="delete-statement-limitations"></a>ELIMINAR las limitaciones de instrucción
La instrucción DELETE no se admite para el controlador de Microsoft Excel o texto. Tenga en cuenta que la instrucción INSERT es compatible con el controlador de texto.  
  
 El controlador dBASE no admite el empaquetado de una tabla para quitar valores de "eliminar".  
  
 Para que el controlador de Paradox eliminar una fila de una tabla, la tabla debe tener un índice único (clave principal Paradox).
