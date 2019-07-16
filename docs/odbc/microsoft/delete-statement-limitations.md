---
title: Limitaciones de la instrucción DELETE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE statement limitations [ODBC]
- ODBC SQL grammar, DELETE statement limitations
ms.assetid: 084761fe-e65b-4f38-ba4f-69884b2a7700
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eb2587f733f5042436144f7865627fee576e3d9c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096307"
---
# <a name="delete-statement-limitations"></a>ELIMINAR las limitaciones de instrucción
No se admite la instrucción DELETE para el controlador de Microsoft Excel o texto. Tenga en cuenta que la instrucción INSERT se admite para el controlador de texto.  
  
 El controlador de dBASE no admite el empaquetado de una tabla para quitar los valores "eliminado".  
  
 Para que el controlador de Paradox eliminar una fila de una tabla, la tabla debe tener un índice único (clave principal de Paradox).
