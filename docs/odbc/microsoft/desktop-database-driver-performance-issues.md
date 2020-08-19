---
description: Problemas de rendimiento del controlador de base de datos de escritorio
title: Problemas de rendimiento del controlador de base de datos de escritorio | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20c21c493d81df6afb4a338675f86ad96ccfab68
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449557"
---
# <a name="desktop-database-driver-performance-issues"></a>Problemas de rendimiento del controlador de base de datos de escritorio
Para garantizar la compatibilidad con las aplicaciones ANSI existentes, los tipos de datos SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR se exponen como SQL_CHAR, SQL_VARCHAR y SQL_LONGVARCHAR para orígenes de datos de Microsoft Access 4,0 o superior. Los orígenes de datos no devuelven tipos de datos de caracteres ANCHOs, pero los datos todavía deben enviarse a Jet en formato de caracteres anchos. Es importante comprender que la conversión se realizará si un SQL_C_CHAR parámetro o columna de resultados se enlaza a un tipo de datos SQL_CHAR en una aplicación ANSI.  
  
 Esta conversión puede ser especialmente ineficaz en lo que se refiere a la memoria cuando se enlaza un tipo SQL_C_CHAR a un parámetro de tipo LONGVARCHAR. Dado que el motor jet 4,0 no puede transmitir datos de parámetros LONGTEXT, se debe asignar un búfer de conversión Unicode que sea el doble del tamaño del búfer ANSI SQL_C_CHAR. El mecanismo más eficaz consiste en que la aplicación realice la conversión Unicode y enlace el parámetro como de tipo SQL_C_WCHAR. Cuando un parámetro se marca como datos en ejecución y los datos se proporcionan en varias llamadas a SQLPutData, se aumenta un búfer de datos LONGTEXT. Una manera de evitar el gasto en el crecimiento de este búfer "Put Data" es proporcionar una longitud opcional a través de SQL_DATA_AT_EXEC_LEN (x), donde *x* es la longitud esperada de bytes. Esto inicializará el tamaño de un búfer PutData interno en *x* bytes.  
  
> [!NOTE]  
>  Una manera eficaz de insertar o actualizar datos largos se puede realizar con **SQLBulkOperations ()** o **SQLSetPos ()** y establecer los datos largos en SQL_DATA_AT_EXEC. (En este caso, se omite EXEC_LEN). Los datos se pueden transmitir en fragmentos mediante una llamada a **SQLPutData** varias veces, lo que, de hecho, anexará los datos a la tabla.  
  
 Cuando una aplicación que usa una base de datos Jet 3,5 a través de los controladores de base de datos de Microsoft ODBC Desktop se actualiza a la versión 4,0, se puede producir una degradación del rendimiento y un mayor tamaño del espacio de trabajo. Esto se debe a que, cuando se trata de una versión 3. la base de datos *x* se abre con el controlador de la nueva versión 4,0 y carga jet 4,0. Cuando jet 4,0 abre la base de datos y observa que la base de datos es un 3. *x* versión, carga un controlador ISAM instalable que es equivalente a cargar también el motor Jet 3,5. Para eliminar el rendimiento y la penalización del tamaño, el inyector 3. la base de datos *x* debe compactarse en una base de datos de formato jet 4,0. Esto eliminará la carga de dos motores jet y minimizará la ruta de acceso del código a los datos.  
  
 Además, el motor jet 4,0 es un motor de Unicode. Todas las cadenas se almacenan y se manipulan en Unicode. Cuando una aplicación ANSI tiene acceso a un Jet 3. *x* a través del motor jet 4,0, los datos se convierten de ANSI a Unicode y de nuevo a ANSI. Si la base de datos se actualiza al formato de la versión 4,0, las cadenas se convierten a Unicode, quitando un nivel de conversión de cadena y minimizando la ruta de acceso del código a los datos, pasando por un solo motor jet.
