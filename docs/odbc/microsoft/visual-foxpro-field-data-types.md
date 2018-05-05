---
title: Tipos de datos de campo de Visual FoxPro | Documentos de Microsoft
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
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2bb370e2e27d2c058b93bbe25024b33947994d3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de datos de campo de Visual FoxPro
En la tabla siguiente se enumera los valores para la *FieldType* argumento en ALTER TABLE y CREATE TABLE e indica si *nFieldWidth* y *nPrecision* argumentos son Obligatorio.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Doble|  
|C|N|-|Campo de caracteres de ancho *n*|  
|D|-|-|Date|  
|F|N|d|Flotante campo numérico de ancho *n* con *d.* posiciones decimales|  
|G|-|-|General|  
|I|-|-|Integer|  
|L|-|-|Lógico|  
|M|-|-|Memorándum|  
|N|N|d|Campo numérico de ancho *n* con *d.* posiciones decimales|  
|T|-|-|DateTime|  
|S|-|-|Moneda|
