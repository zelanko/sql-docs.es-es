---
title: Los descriptores de copia | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e2e5897afc3673a21396e256df04d25008c8cdf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301674"
---
# <a name="copying-descriptors"></a>Descriptores de copias
Se llama a la función **SQLCopyDesc** para copiar los campos de un descriptor en otro descriptor. Los campos solo se pueden copiar en un descriptor de aplicación o en IPD, pero no en IRD. Los campos se pueden copiar desde cualquier tipo de descriptor. Solo se copian los campos definidos para los descriptores de origen y de destino. **SQLCopyDesc** no copia el campo de SQL_DESC_ALLOC_TYPE porque no se puede cambiar el tipo de asignación de un descriptor. Los campos copiados sobrescriben los campos existentes.  
  
 Un ARD en un identificador de instrucción puede servir como APD en otro identificador de instrucción. Esto permite que una aplicación copie filas entre tablas sin copiar datos en el nivel de la aplicación. Para ello, se reutiliza un descriptor de fila que describe una fila capturada de una tabla como un descriptor de parámetros para un parámetro en una instrucción INSERT. El tipo de información de SQL_MAX_CONCURRENT_ACTIVITIES debe ser mayor que 1 para que esta operación se realice correctamente.
