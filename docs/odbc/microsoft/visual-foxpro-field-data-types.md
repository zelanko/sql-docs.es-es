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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72313e0269c93bca9cb2561d89604c3c88c8567b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304806"
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de datos de campo de Visual FoxPro
En la tabla siguiente se muestran los valores para el argumento *FieldType* en alter table y CREATE TABLE e indica si son necesarios los argumentos *nFieldWidth* y *nPrecision* .  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Descripción|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Doble|  
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
