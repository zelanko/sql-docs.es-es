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
ms.openlocfilehash: 217058bf328677bf375d346ae7201c6eb81efa4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68087953"
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de datos de campo de Visual FoxPro
En la tabla siguiente se enumera los valores para el *FieldType* argumento en ALTER TABLE y CREATE TABLE e indica si *nFieldWidth* y *nPrecision* argumentos son Obligatorio.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Descripción|  
|-----------------|-------------------|------------------|-----------------|  
|b|-|d|Double|  
|C|N|-|Campo de caracteres de ancho *n*|  
|D|-|-|Date|  
|F|N|d|Flotante a un campo numérico de ancho *n* con *d.* posiciones decimales|  
|G|-|-|General|  
|I|-|-|Entero|  
|L|-|-|Lógico|  
|M|-|-|Memorándum|  
|N|N|d|Campo numérico de ancho *n* con *d.* posiciones decimales|  
|T|-|-|DateTime|  
|Y|-|-|Currency|
