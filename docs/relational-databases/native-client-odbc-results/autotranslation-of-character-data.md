---
title: Traducción automática de datos de caracteres | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 42c749ee8f42d3ed93ab4936115c7eee68dbd834
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39542375"
---
# <a name="autotranslation-of-character-data"></a>Traducción automática de datos de caracteres
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Datos de caracteres, como ANSI de caracteres variables declaradas con SQL_C_CHAR o los datos almacenados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando el **char**, **varchar**, o **texto** tipos de datos, puede representan sólo un número limitado de caracteres. Los datos de caracteres almacenados que usan un byte por carácter solamente pueden representar 256 caracteres. Los valores almacenados en variables SQL_C_CHAR se interpretan utilizando la página de códigos ANSI (ACP) del equipo cliente. Los valores almacenados mediante **char**, **varchar**, o **texto** tipos de datos en el servidor se evalúan mediante la ACP del servidor.  
  
 Si el servidor y el cliente tienen la misma ACP, no tienen problemas para interpretar los valores almacenados en SQL_C_CHAR, **char**, **varchar**, o **texto** objetos. Si el servidor y cliente tienen ACP diferentes, los datos SQL_C_CHAR del cliente se pueden interpretar como un carácter diferente en el servidor si se usa en **char**, **varchar**, o **texto** columnas, variables o parámetros. Por ejemplo, un byte de caracteres que contiene el valor 0xA5 se interpreta como el carácter Ñ en un equipo mediante la página de códigos 437 y se interpreta como el yen firmar (¥) en un equipo que ejecuta la página de códigos 1252.  
  
 Los datos Unicode se almacenan utilizando dos bytes por carácter. Todos los caracteres extendidos quedan cubiertos por la especificación Unicode, de modo que todos los caracteres Unicode son interpretados de igual manera por todos los equipos.  
  
 La característica de traducción automática de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client intenta minimizar los problemas de mover datos de caracteres entre un cliente y un servidor que tienen páginas de códigos diferentes. AutoTranslate se puede establecer en la cadena de conexión de [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md), en la cadena de configuración de [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md), o al configurar orígenes de datos para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC de Native Client controlador mediante el Administrador ODBC.  
  
 Si AutoTranslate está establecido en "no", se realiza ninguna conversión en los datos movidos entre variables SQL_C_CHAR del cliente y **char**, **varchar**, o **texto** columnas, variables, o los parámetros de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. Los modelos de bits se pueden interpretar de manera diferente en los equipos cliente y servidor si los datos contienen caracteres extendidos y los dos equipos tienen páginas de códigos diferentes. Los datos se interpretarán del mismo modo si ambos equipos tienen la misma página de códigos.  
  
 Si AutoTranslate está establecido en "Sí", la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client utiliza Unicode para convertir los datos movidos entre variables SQL_C_CHAR del cliente y **char**, **varchar**, o **texto** columnas, variables o parámetros en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos:  
  
-   Cuando se envían los datos de una variable SQL_C_CHAR del cliente un **char**, **varchar**, o **texto** columna, variable o parámetro en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos ODBC controlador primero convierte de SQL_C_CHAR a Unicode mediante la ACP del cliente, a continuación, de Unicode a carácter mediante la ACP del servidor.  
  
-   Cuando los datos se envían desde un **char**, **varchar**, o **texto** columna, variable o parámetro en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos a una variable SQL_C_CHAR del cliente, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Controlador ODBC de cliente nativo primero convierte de carácter a Unicode mediante la ACP del servidor, a continuación, de Unicode a SQL_C_CHAR utilizando la ACP del cliente.  
  
 Dado que todas estas conversiones son realizadas por el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecución de controlador ODBC de Native Client en el cliente, la ACP del servidor debe ser una de las páginas de códigos instaladas en el equipo cliente.  
  
 Al realizar las conversiones de caracteres mediante Unicode, se asegura la conversión correcta de todos los caracteres que existen en ambas páginas de códigos. Si un carácter existe en una página de códigos pero no en otra, el carácter no se podrá representar en la página de códigos de destino. Por ejemplo, la página de códigos 1252 tiene el símbolo de marca registrada (®), mientras que la página de códigos 437 no lo tiene.  
  
 El valor AutoTranslate no tiene ningún efecto en estas conversiones:  
  
-   Mover datos entre variables de cliente SQL_C_CHAR de caracteres y Unicode **nchar**, **nvarchar**, o **ntext** columnas, variables o parámetros en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos.  
  
-   Mover datos entre variables SQL_C_WCHAR de Unicode del cliente y el carácter **char**, **varchar**, o **texto** columnas, variables o parámetros en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos.  
  
 Los datos siempre se deben convertir cuando se pasan de caracteres a Unicode.  
  
## <a name="see-also"></a>Vea también  
 [Procesar resultados &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/processing-results-odbc.md)   
 [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)  
  
  
