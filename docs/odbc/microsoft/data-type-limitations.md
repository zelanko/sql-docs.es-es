---
title: Limitaciones de los tipos de datos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280675"
---
# <a name="data-type-limitations"></a>Limitaciones del tipo de datos
Los controladores de base de datos de Microsoft ODBC Desktop imponen las siguientes limitaciones en los tipos de datos:  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|Todos los tipos de datos|Los errores de conversión de tipos pueden dar lugar a que la columna afectada se establezca en NULL.|  
|BINARY|Al crear una columna BINARIa de longitud cero, se devuelve realmente una columna BINARIa de 255 bytes.|  
|DATE|El tipo de datos DATE no se puede convertir en otro tipo de datos (o en sí mismo) mediante la función CONVERT.|  
|DECIMAL (numérico exacto)|No se admite.|  
|Tipos de datos de punto flotante|El número de posiciones decimales en un número de punto flotante puede estar limitado por el formato de número establecido en la sección internacional del panel de control de Windows.|  
|NUMERIC|Admite la precisión máxima y una escala de 28.|  
|timestamp|La función CONVERT no puede convertir el tipo de datos TIMESTAMP en sí mismo.|  
|TINYINT|Los valores TINYINT siempre están sin signo.|  
|Cadenas de longitud cero|Cuando se usa dBASE, Microsoft Excel, Paradox o Textdriver, al insertar una cadena de longitud cero en una columna se inserta realmente un valor NULL.|
