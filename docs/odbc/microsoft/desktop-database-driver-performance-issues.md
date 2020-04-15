---
title: Problemas de rendimiento del controlador de base de datos de escritorio ? Microsoft Docs
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
ms.openlocfilehash: a819d99a995fd7b287beb66b94f1df526e05f201
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303506"
---
# <a name="desktop-database-driver-performance-issues"></a>Problemas de rendimiento del controlador de base de datos de escritorio
Para garantizar la compatibilidad con las aplicaciones ANSI existentes, los tipos de datos SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR se exponen como SQL_CHAR, SQL_VARCHAR y SQL_LONGVARCHAR para orígenes de datos de Microsoft Access 4.0 o superior. Los orígenes de datos no devuelven tipos de datos WIDE CHAR, pero los datos aún deben enviarse a Jet en forma de Carácter ancho. Es importante comprender que la conversión tendrá lugar si un parámetro de SQL_C_CHAR o columna de resultado está enlazado a un tipo de datos SQL_CHAR en una aplicación ANSI.  
  
 Esta conversión puede ser especialmente ineficiente en términos de memoria cuando un tipo de SQL_C_CHAR está enlazado a un parámetro de tipo LONGVARCHAR. Puesto que el motor Jet 4.0 no puede transmitir datos de parámetros LONGTEXT, se debe asignar un búfer de conversión UNICODE que sea el doble del tamaño del búfer ANSI SQL_C_CHAR. El mecanismo más eficaz es que la aplicación realice la conversión UNICODE y enlace el parámetro como tipo SQL_C_WCHAR. Cuando un parámetro se marca como datos en ejecución y los datos se proporcionan en varias llamadas a SQLPutData, se genera un búfer de datos de texto largo. Una manera de evitar el gasto de hacer crecer este búfer "Put Data" es proporcionar una longitud opcional a través de SQL_DATA_AT_EXEC_LEN(x), donde *x* es la longitud esperada de bytes. Esto inicializará el tamaño de un búfer PutData interno en *x* bytes.  
  
> [!NOTE]  
>  Una forma eficaz de insertar o actualizar datos largos se puede lograr mediante **SQLBulkOperations()** o **SQLSetPos()** y estableciendo los datos largos en SQL_DATA_AT_EXEC. (EXEC_LEN se ignora en este caso.) Los datos se pueden transmitir en fragmentos llamando a **SQLPutData** varias veces, lo que anexará eficazmente los datos a la tabla.  
  
 Cuando una aplicación que usa una base de datos Jet 3.5 a través de los controladores de base de datos de escritorio ODBC de Microsoft se actualiza a la versión 4.0, puede producirse una degradación del rendimiento y un mayor tamaño del conjunto de trabajo. Esto se debe a que cuando se trata de una versión 3. *x* base de datos se abre utilizando el nuevo controlador de la versión 4.0, carga Jet 4.0. Cuando Jet 4.0 abre la base de datos y ve que la base de datos es un 3. *x* versión, carga un controlador ISAM instalable que es equivalente a cargar el motor Jet 3.5 también. Para eliminar la penalización de rendimiento y tamaño, el Jet 3. *x* base de datos debe compactarse en una base de datos de formato Jet 4.0. Esto eliminará la carga de dos motores Jet y minimizará la ruta de acceso del código a los datos.  
  
 Además, el motor Jet 4.0 es un motor Unicode. Todas las cadenas se almacenan y manipulan en Unicode. Cuando una aplicación ANSI accede a un Jet 3. *x* base de datos a través del motor Jet 4.0, los datos se convierten de ANSI a Unicode y de nuevo a ANSI. Si la base de datos se actualiza al formato de la versión 4.0, las cadenas se convierten a Unicode, eliminando un nivel de conversión de cadenas, así como minimizando la ruta de acceso de código a los datos pasando por un solo motor Jet.
