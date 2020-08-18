---
description: Tipos de datos de campo de Visual FoxPro
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
ms.openlocfilehash: 65410f16367af8764e8572c58e53831f3f7b9cda
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449057"
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de datos de campo de Visual FoxPro
En la tabla siguiente se muestran los valores para el argumento *FieldType* en alter table y CREATE TABLE e indica si son necesarios los argumentos *nFieldWidth* y *nPrecision* .  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Descripción|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|Campo de carácter de ancho *n*|  
|D|-|-|Date|  
|F|N|d|Campo numérico flotante de ancho *n* con posiciones decimales de *d*|  
|G|-|-|General|  
|I|-|-|Entero|  
|L|-|-|Lógico|  
|M|-|-|Memorándum|  
|N|N|d|Campo numérico de ancho *n* con posiciones decimales de *d*|  
|T|-|-|DateTime|  
|Y|-|-|Moneda|
