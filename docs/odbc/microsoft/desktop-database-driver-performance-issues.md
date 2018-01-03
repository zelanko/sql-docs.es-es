---
title: Problemas de rendimiento del controlador de base de datos de escritorio | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], performance
- desktop database drivers [ODBC], performance
- Jet-based ODBC drivers [ODBC], performance
ms.assetid: 1a4c4b7e-9744-411f-9b6e-06dfdad92cf7
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67379ee540aecb691122d91b42776b0c9d990b1d
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="desktop-database-driver-performance-issues"></a>Problemas de rendimiento del controlador de base de datos de escritorio
Para garantizar la compatibilidad con las aplicaciones existentes de ANSI, los tipos de datos SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR se exponen como SQL_CHAR, SQL_VARCHAR y SQL_LONGVARCHAR para Microsoft Access 4.0 o superior orígenes de datos. Los orígenes de datos no devuelven tipos de datos de carácter ancho, pero los datos todavía se deben enviar a Jet en forma de carácter ancho. Es importante comprender que conversión llevará a cabo si una columna de parámetro o el resultado SQL_C_CHAR está enlazada a un tipo de datos SQL_CHAR en una aplicación de ANSI.  
  
 Esta conversión puede ser especialmente eficaz en cuanto a memoria cuando un tipo SQL_C_CHAR se enlaza a un parámetro de tipo LONGVARCHAR. Puesto que el motor Jet 4.0 es capaz de flujo de datos del parámetro LONGTEXT, se debe asignar un búfer de conversión UNICODE que es dos veces el tamaño del búfer de ANSI SQL_C_CHAR. Es el mecanismo más eficiente para que la aplicación realizar la conversión de UNICODE y enlazar el parámetro como tipo SQL_C_WCHAR. Cuando un parámetro se marca como datos en ejecución y los datos se proporcionan en varias llamadas a SQLPutData, un búfer de datos longtext es incrementar. Una manera de evitar el gasto de crecimiento este búfer de "Colocar datos" es proporcionar una longitud opcional a través de SQL_DATA_AT_EXEC_LEN(x), donde *x* es la longitud esperada de bytes. Esto inicializará en el tamaño de un búfer interno de PutData a *x* bytes.  
  
> [!NOTE]  
>  Una manera eficaz para insertar o actualizar datos de tipo long puede realizarse mediante **SQLBulkOperations()** o **SQLSetPos()** y establecer los datos de tipo long en SQL_DATA_AT_EXEC. (En este caso se omite EXEC_LEN.) Se pueden transmitir datos en fragmentos mediante una llamada a **SQLPutData** varias veces, eficazmente que anexarán los datos a la tabla.  
  
 Cuando una aplicación con una base de datos de Jet 3.5 a través de los controladores de base de datos de Microsoft ODBC Desktop se actualiza a la versión 4.0, pueden producirse una degradación de rendimiento y un mayor tamaño de conjunto de trabajo. Esto es porque cuando hay una versión 3. *x* base de datos se abre mediante la nueva versión 4.0 del controlador, carga Jet 4.0. Cuando se abre la base de datos de Jet 4.0 y ve la base de datos es un 3. *x* versión, carga un controlador ISAM instalable que es equivalente a cargar el motor Jet 3.5 también. Para quitar la penalización de rendimiento y el tamaño, el 3 de Jet. *x* base de datos se debe compactar en una base de datos de formato de Jet 4.0. Esto eliminará la carga dos motores de Jet y minimizar la ruta de acceso del código a los datos.  
  
 Además, el motor Jet 4.0 es un motor de Unicode. Todas las cadenas se almacenan y manipulan en Unicode. Cuando una aplicación ANSI tiene acceso a un 3 de Jet. *x* base de datos a través del motor Jet 4.0, los datos se convierte de ANSI a Unicode y de vuelta a ANSI. Si la base de datos se actualiza a la versión 4.0 del formato, las cadenas se convierten a Unicode, quitar un nivel de conversión de cadenas como la ruta de acceso del código a los datos, vaya a través de un solo motor Jet.
