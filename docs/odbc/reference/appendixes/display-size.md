---
title: Tamaño de pantalla | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- display size of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- SQL data types [ODBC], column characteristics
ms.assetid: 9f7f766f-2492-463c-aab7-f2476e222042
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f0cd835b31863fa8427f4cb175c66ded5f7e308
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="display-size"></a>Tamaño de presentación
El tamaño de presentación de una columna es el número máximo de caracteres necesarios para mostrar los datos en formato de carácter. En la tabla siguiente define el tamaño de presentación para cada tipo de datos SQL de ODBC.  
  
|Identificador de tipo SQL|Tamaño de presentación|  
|-------------------------|------------------|  
|Todos los tipos de caracteres [a]|Define (para tipos fijos) o máximo (para los tipos de variable) número de caracteres necesarios para mostrar los datos en formato de carácter.|  
|SQL_NUMERIC SQL_DECIMAL DE ODBC|La precisión de la columna más 2 (un inicio de sesión, *precisión* dígitos y un separador decimal). Por ejemplo, el tamaño de presentación de una columna definida como NUMERIC(10,3) es 12.|  
|SQL_BIT|1 (1 dígito).|  
|SQL_TINYINT|4 si firmado (un inicio de sesión y 3 dígitos) o 3 si sin signo (3 dígitos).|  
|SQL_SMALLINT|6 si firmado (un inicio de sesión y 5 dígitos) o 5 si sin signo (5 dígitos).|  
|SQL_INTEGER|11 si firmado (un inicio de sesión y 10 dígitos) o 10 si sin signo (10 dígitos).|  
|SQL_BIGINT|20 (un inicio de sesión y 19 dígitos si firmado o 20 dígitos si sin signo).|  
|SQL_REAL|14 (un inicio de sesión, 7 dígitos, un separador decimal, la letra *E*, un inicio de sesión y 2 dígitos).|  
|SQL_FLOAT SQL_DOUBLE|24 (un inicio de sesión, 15 dígitos, un separador decimal, la letra *E*, un inicio de sesión y 3 dígitos).|  
|Todos los tipos binarios [a]|Definido o máximo (para los tipos de variable) el tiempo de longitud de la columna 2. (Cada byte binario se representa mediante un número hexadecimal de 2 dígitos).|  
|SQL_TYPE_DATE|10 (una fecha en el formato *aaaa-mm-dd*).|  
|SQL_TYPE_TIME|8 (una hora en el formato *hh*)<br /><br /> O bien<br /><br /> 9 + *s* (una hora en el formato *hh*[.fff...], donde *s* es la precisión de fracciones de segundo).|  
|SQL_TYPE_TIMESTAMP|19 (para una marca de tiempo en el *aaaa-mm-dd hh* formato)<br /><br /> O bien<br /><br /> 20 + *s* (para una marca de tiempo en el *aaaa-mm-dd hh*formato [.fff...], donde *s* es la precisión de fracciones de segundo).|  
|Todos los tipos de datos de intervalo|Vea [longitud de tipo de datos de intervalo](../../../odbc/reference/appendixes/interval-data-type-length.md).|  
|SQL_GUID|36 (el número de caracteres en el *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee* formato|  
  
 [a] si el controlador no puede determinar la longitud de columna o parámetro de tipos de variables, devuelve SQL_NO_TOTAL.
