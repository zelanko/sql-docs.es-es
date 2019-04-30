---
title: Tamaño de presentación | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2c7d4a14a6afc2d716e85e687cbae1a202a596d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63241250"
---
# <a name="display-size"></a>Tamaño de presentación
El tamaño de presentación de una columna es el número máximo de caracteres necesario para mostrar datos en formato de caracteres. En la tabla siguiente se define el tamaño de presentación para cada tipo de datos SQL de ODBC.  
  
|Identificador de tipo SQL|Tamaño de presentación|  
|-------------------------|------------------|  
|Todos los tipos de caracteres [a]|Máximo (tipos de variable) o el definido (para tipos fijos) número de caracteres necesarios para mostrar los datos en formato de caracteres.|  
|SQL_DECIMAL SQL_NUMERIC|La precisión de la columna más 2 (un inicio de sesión, *precisión* dígitos y un separador decimal). Por ejemplo, el tamaño de presentación de una columna definida como NUMERIC(10,3) es 12.|  
|SQL_BIT|1 (1 dígito).|  
|SQL_TINYINT|4 si ha iniciado (un inicio de sesión y 3 dígitos) o 3 Si no tiene signo (3 dígitos).|  
|SQL_SMALLINT|6 Si ha iniciado (un inicio de sesión y 5 dígitos) o 5 si no tiene signo (5 dígitos).|  
|SQL_INTEGER|11 Si ha iniciado (un inicio de sesión y 10 dígitos) o 10 si no tiene signo (10 dígitos).|  
|SQL_BIGINT|20 (un inicio de sesión y 19 dígitos si ha iniciado o 20 dígitos si no tiene signo).|  
|SQL_REAL|14 (un inicio de sesión, 7 dígitos, un separador decimal, la letra *E*, un inicio de sesión y 2 dígitos).|  
|SQL_FLOAT SQL_DOUBLE|24 (un signo, 15 dígitos, un separador decimal, la letra *E*, un inicio de sesión y 3 dígitos).|  
|Todos los tipos binarios [a]|Define o máximo (tipos de variable) el tiempo de longitud de la columna 2. (Cada byte binario está representado por un número hexadecimal de 2 dígitos).|  
|SQL_TYPE_DATE|10 (una fecha en el formato *aaaa-mm-dd*).|  
|SQL_TYPE_TIME|8 (una hora en el formato *hh: mm:*)<br /><br /> O bien<br /><br /> 9 + *s* (una hora en el formato *hh: mm:*[.fff...], donde *s* es la precisión de fracciones de segundo).|  
|SQL_TYPE_TIMESTAMP|19 (para una marca de tiempo en el *aaaa-mm-dd hh: mm:* formato)<br /><br /> O bien<br /><br /> 20 + *s* (para una marca de tiempo en el *aaaa-mm-dd hh: mm:* formato [.fff...], donde *s* es la precisión de fracciones de segundo).|  
|Todos los tipos de datos interval|Consulte [longitud de tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md).|  
|SQL_GUID|36 (el número de caracteres en el *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* formato|  
  
 [a] si el controlador no puede determinar la longitud de columna o parámetro de tipos de variables, devolverá SQL_NO_TOTAL.
