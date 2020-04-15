---
title: Traducción automática de datos de caracteres ( Autotranslation of Character Data) Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC], autotranslating character data
- data types [ODBC], autotranslating character data
- ACPs
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- AutoTranslate feature
- ANSI code pages
- character data autotranslation [ODBC]
- autotranslating character data
- SQL Server Native Client ODBC driver, data types
- ODBC data types, autotranslating character data
ms.assetid: 86a8adda-c5ad-477f-870f-cb370c39ee13
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2a8672f748af8d643fa39038be030efa5d434dc8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297887"
---
# <a name="autotranslation-of-character-data"></a>Traducción automática de datos de caracteres
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Los datos de caracteres, como las variables [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de caracteres ANSI declaradas con SQL_C_CHAR o los datos almacenados en los tipos de datos **char**, **varchar**o **text,** solo pueden representar un número limitado de caracteres. Los datos de caracteres almacenados que usan un byte por carácter solamente pueden representar 256 caracteres. Los valores almacenados en variables SQL_C_CHAR se interpretan utilizando la página de códigos ANSI (ACP) del equipo cliente. Los valores almacenados mediante los tipos de datos **char**, **varchar**o **text** en el servidor se evalúan mediante el ACP del servidor.  
  
 Si tanto el servidor como el cliente tienen el mismo ACP, no tienen problemas para interpretar los valores almacenados en SQL_C_CHAR, **char**, **varchar**u objetos de **texto.** Si el servidor y el cliente tienen API diferentes, los datos SQL_C_CHAR del cliente se pueden interpretar como un carácter diferente en el servidor si se utilizan en columnas, variables o parámetros **char**, **varchar**o **text.** Por ejemplo, un byte de caracteres que contiene el valor 0xA5 se interpreta como el carácter . en un equipo mediante la página de códigos 437 y se interpreta como el signo de yen (o) en un equipo que ejecuta la página de códigos 1252.  
  
 Los datos Unicode se almacenan utilizando dos bytes por carácter. Todos los caracteres extendidos quedan cubiertos por la especificación Unicode, de modo que todos los caracteres Unicode son interpretados de igual manera por todos los equipos.  
  
 La característica AutoTranslate [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del controlador ODBC de Native Client intenta minimizar los problemas al mover datos de caracteres entre un cliente y un servidor que tienen páginas de códigos diferentes. AutoTranslate se puede establecer en la cadena de conexión de [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md), en la cadena [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de configuración de [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)o al configurar orígenes de datos para el controlador ODBC de Native Client mediante el Administrador ODBC.  
  
 Cuando AutoTranslate se establece en "no", no se realizan conversiones en los datos movidos entre SQL_C_CHAR variables [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en las columnas de cliente y **char**, **varchar**o **texto,** variables o parámetros de una base de datos. Los modelos de bits se pueden interpretar de manera diferente en los equipos cliente y servidor si los datos contienen caracteres extendidos y los dos equipos tienen páginas de códigos diferentes. Los datos se interpretarán del mismo modo si ambos equipos tienen la misma página de códigos.  
  
 Cuando AutoTranslate se establece en "yes", [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el controlador ODBC de Native Client utiliza Unicode para convertir datos movidos entre SQL_C_CHAR variables en el cliente y **char**, **varchar**o columnas de **texto,** variables o parámetros en una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos:  
  
-   Cuando los datos se envían desde una variable SQL_C_CHAR en el cliente a **una**columna de **texto,** variable o columna de texto char , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varchar**o en una base de datos, el controlador ODBC convierte primero de SQL_C_CHAR a Unicode mediante el ACP del cliente y, a continuación, de Unicode a carácter mediante el ACP del servidor.  
  
-   Cuando los datos se envían desde **una**columna de **texto,** variable o columna char , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **varchar**o text en una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos a una variable SQL_C_CHAR en el cliente, el controlador ODBC de Native Client primero convierte de carácter a Unicode mediante el ACP del servidor y, a continuación, de Unicode a SQL_C_CHAR mediante el ACP del cliente.  
  
 Dado que todas estas conversiones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las realiza el controlador ODBC de Native Client que se ejecuta en el cliente, el servidor ACP debe ser una de las páginas de códigos instaladas en el equipo cliente.  
  
 Al realizar las conversiones de caracteres mediante Unicode, se asegura la conversión correcta de todos los caracteres que existen en ambas páginas de códigos. Si un carácter existe en una página de códigos pero no en otra, el carácter no se podrá representar en la página de códigos de destino. Por ejemplo, la página de códigos 1252 tiene el símbolo de marca registrada (®), mientras que la página de códigos 437 no lo tiene.  
  
 El valor AutoTranslate no tiene ningún efecto en estas conversiones:  
  
-   Mover datos entre variables de cliente SQL_C_CHAR de caracteres y columnas **Unicode nchar**, **nvarchar**o **ntext,** variables o parámetros en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos.  
  
-   Mover datos entre Unicode SQL_C_WCHAR variables de cliente y caracteres **char** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **varchar**o columnas de **texto,** variables o parámetros en bases de datos.  
  
 Los datos siempre se deben convertir cuando se pasan de caracteres a Unicode.  
  
## <a name="see-also"></a>Consulte también  
 [Procesamiento de resultados &#40;&#41;ODBC](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Collation y soporte Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
