---
title: Tipos de datos de campo de Visual FoxPro | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2b4dbb88985b114e0e2f89c4a3f57d8dae4c9210
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de datos de campo de Visual FoxPro
En la tabla siguiente se enumera los valores para la *FieldType* argumento en ALTER TABLE y CREATE TABLE e indica si *nFieldWidth* y *nPrecision* argumentos son Obligatorio.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Description|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Doble|  
|C|N|-|Campo de caracteres de ancho*n*|  
|D|-|-|Date|  
|F|N|d|Flotante campo numérico de ancho  *n*  con *d.* posiciones decimales|  
|G|-|-|General|  
|I|-|-|Integer|  
|L|-|-|Lógico|  
|M|-|-|Memorándum|  
|N|N|d|Campo numérico de ancho  *n*  con *d.* posiciones decimales|  
|T|-|-|DateTime|  
|S|-|-|Moneda|
