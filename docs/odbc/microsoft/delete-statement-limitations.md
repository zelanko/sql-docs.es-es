---
title: Limitaciones de la declaración DELETE (DELETE Statement Limitations) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 365b54ab8c0678253e184b397f1f71e39aed3b9b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303536"
---
# <a name="delete-statement-limitations"></a>ELIMINAR las limitaciones de instrucción
La instrucción DELETE no se admite para el controlador de Microsoft Excel o Text. Tenga en cuenta que la instrucción INSERT es compatible con el controlador de texto.  
  
 El controlador dBASE no admite el empaquetado de una tabla para quitar los valores "eliminados".  
  
 Para que el controlador Paradox elimine una fila de una tabla, la tabla debe tener un índice único (clave principal de Paradox).
