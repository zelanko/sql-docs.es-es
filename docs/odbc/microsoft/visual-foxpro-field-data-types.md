---
title: Tipos de datos de campo de Visual FoxPro | Microsoft Docs
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
ms.openlocfilehash: 217058bf328677bf375d346ae7201c6eb81efa4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087953"
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de datos de campo de Visual FoxPro
En la tabla siguiente se muestran los valores para el argumento *FieldType* en alter table y CREATE TABLE e indica si son necesarios los argumentos *nFieldWidth* y *nPrecision* .  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Descripción|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|DOUBLE|  
|C|N|-|Campo de carácter de ancho *n*|  
|D|-|-|Date|  
|F|N|d|Campo numérico flotante de ancho *n* con posiciones decimales de *d*|  
|G|-|-|General|  
|I|-|-|Entero|  
|L|-|-|Lógicos|  
|M|-|-|Memorándum|  
|N|N|d|Campo numérico de ancho *n* con posiciones decimales de *d*|  
|T|-|-|DateTime|  
|Y|-|-|Moneda|
