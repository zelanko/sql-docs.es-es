---
title: Descriptores de copias | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d41cd744d39113c556c4ee8bc17411b7992e596
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002140"
---
# <a name="copying-descriptors"></a>Descriptores de copias
El **SQLCopyDesc** función se invoca para copiar los campos de descriptor de uno a otro descriptor. Los campos se pueden copiar solo a un descriptor de aplicación o un IPD, pero no a un IRD. Los campos se pueden copiar desde cualquier tipo de descriptor. Se copian solo los campos que se definen para los descriptores de origen y destino. **SQLCopyDesc** no copia el campo SQL_DESC_ALLOC_TYPE, porque no se puede cambiar el tipo de asignación de un descriptor. Campos copiados sobrescriben los campos existentes.  
  
 Un descartar en el identificador de una instrucción puede servir como el APD en otro identificador de instrucción. Esto permite que una aplicación copiar filas entre las tablas sin copiar los datos en el nivel de aplicación. Para ello, se reutiliza un descriptor de fila que describe una fila de una tabla capturada como un descriptor de parámetro para un parámetro en una instrucción INSERT. El tipo de información SQL_MAX_CONCURRENT_ACTIVITIES debe ser mayor que 1 para esta operación se realice correctamente.
