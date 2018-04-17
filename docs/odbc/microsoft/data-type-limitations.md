---
title: Limitaciones del tipo de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f7be82a89d81f887baf0ae6ef0fe7cd00e72c27
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="data-type-limitations"></a>Limitaciones del tipo de datos
Los controladores de base de datos de Microsoft ODBC Desktop impone las siguientes limitaciones en los tipos de datos:  
  
|Tipo de datos|Description|  
|---------------|-----------------|  
|Todos los tipos de datos|Podrían dar lugar a errores de conversión de tipo en la columna afectada se establece en NULL.|  
|BINARY|Creación de una columna binaria de longitud cero, devuelve realmente una columna binaria de 255 bytes.|  
|DATE|El tipo de datos de fecha no puede convertirse a otro tipo de datos (o propio) mediante la función CONVERT.|  
|DECIMAL (valor numérico exacto)|No compatible.|  
|Tipos de datos de punto flotante|El número de posiciones decimales en un número de punto flotante puede estar limitado por el formato de número que se establece en la sección internacional del Panel de Control de Windows.|  
|NUMERIC|Admite la precisión máxima y una escala de 28.|  
|TIMESTAMP|No se puede convertir el tipo de datos de marca de tiempo a sí misma mediante la función CONVERT.|  
|TINYINT|TINYINT valores siempre son sin signo.|  
|Cadenas de longitud cero|Cuando se utiliza un archivo dBASE, Microsoft Excel, Paradox u Textdriver, insertar una cadena de longitud cero en una columna realmente inserta un valor NULL en su lugar.|
