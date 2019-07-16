---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 660b7c123d0ddd0a3f1b972fa3b1dc153b15ed50
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071931"
---
# <a name="desktop-database-driver-performance-issues"></a>Problemas de rendimiento del controlador de base de datos de escritorio
Para garantizar la compatibilidad con las aplicaciones existentes de ANSI, los tipos de datos SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR se exponen como SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR para Microsoft Access 4.0 o superior orígenes de datos. Los orígenes de datos no devuelven tipos de datos CHAR amplia, pero los datos todavía se deben enviar a Jet en forma de carácter ancho. Es importante comprender que conversión llevará a cabo si una columna de parámetro o el resultado SQL_C_CHAR está enlazada a un tipo de datos SQL_CHAR en una aplicación de ANSI.  
  
 Esta conversión puede ser especialmente eficaz en términos de memoria cuando un tipo SQL_C_CHAR se enlaza a un parámetro de tipo LONGVARCHAR. Puesto que el motor Jet 4.0 no puede flujo de datos del parámetro LONGTEXT, se debe asignar un búfer de conversión UNICODE que es dos veces el tamaño del búfer ANSI SQL_C_CHAR. Es el mecanismo más eficaz para que la aplicación realizar la conversión de UNICODE y enlazar el parámetro como tipo SQL_C_WCHAR. Cuando un parámetro se marca como datos en ejecución y los datos se proporcionan en varias llamadas a SQLPutData, un búfer de datos longtext es crece. Una manera de evitar el gasto de este crecimiento es proporcionar una longitud opcional a través de SQL_DATA_AT_EXEC_LEN(x), búfer de "Datos poner" donde *x* es la longitud de bytes esperada. Esto inicializará el tamaño de un búfer interno de PutData a *x* bytes.  
  
> [!NOTE]  
>  Una manera eficaz para insertar o actualizar datos largos se puede lograr mediante **SQLBulkOperations()** o **SQLSetPos()** y establecer los datos long en SQL_DATA_AT_EXEC. (En este caso se omite EXEC_LEN.) Se pueden transmitir datos en fragmentos mediante una llamada a **SQLPutData** varias veces, lo que efectivamente anexará los datos a la tabla.  
  
 Cuando se actualiza una aplicación con una base de datos de Jet 3.5 a través de los controladores de base de datos de escritorio de Microsoft ODBC a la versión 4.0, pueden producirse alguna degradación del rendimiento y un tamaño mayor de trabajo. Esto es porque cuando una versión 3. *x* base de datos se abre mediante la nueva versión 4.0 del controlador, los cargará Jet 4.0. Cuando se abre la base de datos de Jet 4.0 y ve que la base de datos es un 3. *x* versión, carga un controlador ISAM instalable que es equivalente a cargar el motor Jet 3.5 también. Para quitar la penalización de rendimiento y el tamaño, el 3 de Jet. *x* base de datos se debe compactar en una base de datos de formato de Jet 4.0. Esto eliminará la carga dos motores de Jet y minimizar la ruta de acceso del código a los datos.  
  
 Además, el motor Jet 4.0 es un motor de Unicode. Todas las cadenas se almacenan y manipulan en Unicode. Cuando una aplicación ANSI obtiene acceso a un 3 de Jet. *x* base de datos a través del motor Jet 4.0, los datos se convierte de ANSI a Unicode y volver a ANSI. Si la base de datos se actualiza a la versión 4.0 del formato, las cadenas se convierten a Unicode, quitar un nivel de conversión de cadena así como a minimizar la ruta de acceso del código a los datos a través de un solo motor Jet.
