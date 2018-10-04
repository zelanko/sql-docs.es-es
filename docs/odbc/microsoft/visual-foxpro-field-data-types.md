---
title: Tipos de datos de campo Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 07aa06eae9f1e75a047bdd302754d884790436e1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806134"
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de datos de campo de Visual FoxPro
En la tabla siguiente se enumera los valores para el *FieldType* argumento en ALTER TABLE y CREATE TABLE e indica si *nFieldWidth* y *nPrecision* argumentos son Obligatorio.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Descripción|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Doble|  
|C|N|-|Campo de caracteres de ancho *n*|  
|D|-|-|date|  
|F|N|d|Flotante a un campo numérico de ancho *n* con *d.* posiciones decimales|  
|G|-|-|General|  
|I|-|-|Integer|  
|L|-|-|Lógico|  
|M|-|-|Memorándum|  
|N|N|d|Campo numérico de ancho *n* con *d.* posiciones decimales|  
|T|-|-|DateTime|  
|S|-|-|Moneda|
