---
title: Limitaciones de tipos de datos ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4beaf91a4ead743e3e8a2e32578796baba3c17be
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280675"
---
# <a name="data-type-limitations"></a>Limitaciones del tipo de datos
Los controladores de base de datos de escritorio ODBC de Microsoft imponen las siguientes limitaciones a los tipos de datos:  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|Todos los tipos de datos|Los errores de conversión de tipos pueden dar lugar a que la columna afectada se establezca en NULL.|  
|BINARY|La creación de una columna BINARY de longitud cero devuelve realmente una columna BINARY de 255 bytes.|  
|DATE|El tipo de datos DATE no se puede convertir a otro tipo de datos (o a sí mismo) mediante la función CONVERT.|  
|DECIMAL (numérico exacto)|No compatible.|  
|Tipos de datos de punto flotante|El número de decimales en un número de punto flotante puede estar limitado por el formato numérico establecido en la sección Internacional del Panel de control de Windows.|  
|NUMERIC|Admite la máxima precisión y una escala de 28.|  
|timestamp|El tipo de datos TIMESTAMP no se puede convertir a sí mismo mediante la función CONVERT.|  
|TINYINT|Los valores TINYINT siempre no están firmados.|  
|Cuerdas de longitud cero|Cuando se usa un dBASE, Microsoft Excel, Paradox o Textdriver, insertar una cadena de longitud cero en una columna inserta realmente un NULL en su lugar.|
