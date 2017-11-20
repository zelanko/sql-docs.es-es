---
title: Copiar descriptores | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8cd2ea29713d3bf1e05e76de21397f71dd30c824
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="copying-descriptors"></a>Descriptores de copias
El **SQLCopyDesc** función se invoca para copiar los campos del descriptor de uno a otro descriptor. Campos pueden copiarse únicamente a un descriptor de la aplicación o un IPD, pero no a un IRD. Campos pueden copiarse desde cualquier tipo de descriptor. Solo los campos que se definen para los descriptores de origen y de destino se copian. **SQLCopyDesc** no copia el campo SQL_DESC_ALLOC_TYPE, porque no se puede cambiar el tipo de asignación del descriptor. Campos copiados sobrescriben los campos existentes.  
  
 Un descartar en el identificador de una instrucción puede servir como el APD en otro identificador de instrucción. Esto permite que una aplicación copiar filas entre las tablas sin necesidad de copiar datos en el nivel de aplicación. Para hacer esto, se reutiliza un descriptor de fila que describe una fila recuperada de una tabla como un descriptor de parámetro para un parámetro en una instrucción INSERT. El tipo de información de SQL_MAX_CONCURRENT_ACTIVITIES debe ser mayor que 1 para realizar esta operación correctamente.

