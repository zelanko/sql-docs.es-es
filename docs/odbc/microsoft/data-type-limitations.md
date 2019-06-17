---
title: Limitaciones del tipo de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4ce0eb96832f4a6b9c1953b0a9a9d0af65cb3b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187434"
---
# <a name="data-type-limitations"></a>Limitaciones del tipo de datos
Los controladores de base de datos de escritorio de Microsoft ODBC impone las siguientes limitaciones en los tipos de datos:  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|Todos los tipos de datos|Tipo de conversión pueden dar lugar a errores en la columna afectada que se establece en NULL.|  
|BINARY|Creación de una columna binaria de longitud cero, devuelve realmente una columna binaria 255 bytes.|  
|DATE|El tipo de datos de fecha no puede convertirse a otro tipo de datos (o propio) mediante la función CONVERT.|  
|DECIMAL (numérica exacta)|No compatible.|  
|Tipos de datos de punto flotante|El número de posiciones decimales en un número de punto flotante puede estar limitado por el formato de número establecido en la sección internacional del Panel de Control de Windows.|  
|NUMERIC|Admite la precisión máxima y una escala de 28.|  
|timestamp|No se puede convertir el tipo de datos de marca de tiempo a sí mismo mediante la función CONVERT.|  
|TINYINT|TINYINT valores siempre son sin signo.|  
|Cadenas de longitud cero|Cuando se usa un archivo dBASE, Microsoft Excel, Paradox o Textdriver, insertar una cadena de longitud cero en una columna realmente inserta un valor NULL en su lugar.|
