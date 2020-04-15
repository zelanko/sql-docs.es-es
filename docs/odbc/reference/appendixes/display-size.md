---
title: Tamaño de la pantalla ( Display Size) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 578bf0cbdf2dd1dbd06dd4a248f4efa5eb839916
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307036"
---
# <a name="display-size"></a>Tamaño de presentación
El tamaño de visualización de una columna es el número máximo de caracteres necesarios para mostrar los datos en forma de caracteres. En la tabla siguiente se define el tamaño de presentación para cada tipo de datos SQL ODBC.  
  
|Identificador de tipo SQL|Tamaño de pantalla|  
|-------------------------|------------------|  
|Todos los tipos de caracteres[a]|El número definido (para tipos fijos) o máximo (para tipos variables) de caracteres necesarios para mostrar los datos en forma de carácter.|  
|SQL_DECIMAL SQL_NUMERIC|La precisión de la columna más 2 (un signo, dígitos de *precisión* y un punto decimal). Por ejemplo, el tamaño de visualización de una columna definida como NUMERIC(10,3) es 12.|  
|SQL_BIT|1 (1 dígito).|  
|SQL_TINYINT|4 si está firmado (un signo y 3 dígitos) o 3 si no está firmado (3 dígitos).|  
|SQL_SMALLINT|6 si está firmado (un signo y 5 dígitos) o 5 si no está firmado (5 dígitos).|  
|SQL_INTEGER|11 si está firmado (un signo y 10 dígitos) o 10 si no está firmado (10 dígitos).|  
|SQL_BIGINT|20 (un signo y 19 dígitos si está firmado o 20 dígitos si no está firmado).|  
|SQL_REAL|14 (un signo, 7 dígitos, un punto decimal, la letra *E,* un signo y 2 dígitos).|  
|SQL_FLOAT SQL_DOUBLE|24 (un signo, 15 dígitos, un punto decimal, la letra *E,* un signo y 3 dígitos).|  
|Todos los tipos binarios[a]|La longitud definida o máxima (para tipos variables) de la columna por 2. (Cada byte binario está representado por un número hexadecimal de 2 dígitos.)|  
|SQL_TYPE_DATE|10 (una fecha en el formato *aaaa-mm-dd*).|  
|SQL_TYPE_TIME|8 (una hora en el formato *hh:mm:ss*)<br /><br /> O bien<br /><br /> 9 + *s* (una hora en el formato *hh:mm:ss*[.fff...], donde *s* es la precisión de fracciones de segundo).|  
|SQL_TYPE_TIMESTAMP|19 (para una marca de tiempo en el formato *aaaa-mm-dd hh:mm:ss)*<br /><br /> O bien<br /><br /> 20 + *s* (para una marca de tiempo en el formato *aaaa-mm-dd hh:mm:ss*[.fff...], donde *s* es la precisión de fracciones de segundo).|  
|Todos los tipos de datos de intervalo|Consulte [Longitud del tipo](../../../odbc/reference/appendixes/interval-data-type-length.md)de datos de intervalo .|  
|SQL_GUID|36 (el número de caracteres en el formato *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee*|  
  
 [a] Si el controlador no puede determinar la longitud de columna o parámetro de los tipos de variables, devuelve SQL_NO_TOTAL.
