---
title: Autotraducción de datos de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5182ab1a72caac4181e50df2199f3e0457d3aaac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63200213"
---
# <a name="autotranslation-of-character-data"></a>Traducción automática de datos de caracteres
  Los datos de caracteres, como las variables de caracteres ANSI declarados con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SQL_C_CHAR o los datos almacenados en usando los tipos de datos **Char**, **VARCHAR**o **Text** , pueden representar solo un número limitado de caracteres. Los datos de caracteres almacenados que usan un byte por carácter solamente pueden representar 256 caracteres. Los valores almacenados en variables SQL_C_CHAR se interpretan utilizando la página de códigos ANSI (ACP) del equipo cliente. Los valores almacenados mediante los tipos de datos **Char**, **VARCHAR**o **Text** en el servidor se evalúan mediante la ACP del servidor.  
  
 Si el servidor y el cliente tienen el mismo ACP, no tienen problemas para interpretar los valores almacenados en los objetos SQL_C_CHAR, **Char**, **VARCHAR**o **Text** . Si el servidor y el cliente tienen ACP diferentes, SQL_C_CHAR datos del cliente pueden interpretarse como un carácter diferente en el servidor si se utiliza en columnas, variables o parámetros **Char**, **VARCHAR**o **Text** . Por ejemplo, un byte de caracteres que contiene el valor 0xA5 se interpreta como el carácter?? en un equipo que usa la página de códigos 437 y se interpreta como el signo del yen (??) en un equipo que ejecuta la página de códigos 1252.  
  
 Los datos Unicode se almacenan utilizando dos bytes por carácter. Todos los caracteres extendidos quedan cubiertos por la especificación Unicode, de modo que todos los caracteres Unicode son interpretados de igual manera por todos los equipos.  
  
 La característica autotranslate del controlador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ODBC de Native Client intenta minimizar los problemas de movimiento de datos de caracteres entre un cliente y un servidor que tienen páginas de códigos diferentes. Autotranslate se puede establecer en la cadena de conexión de [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md), en la cadena de configuración de [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md), o al configurar orígenes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos para el controlador ODBC de Native Client mediante el administrador de ODBC.  
  
 Cuando autotranslate se establece en "no", no se realiza ninguna conversión en los datos que se mueven entre SQL_C_CHAR variables en el cliente y las columnas, variables o parámetros **Char**, **VARCHAR**o **Text** de una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos. Los modelos de bits se pueden interpretar de manera diferente en los equipos cliente y servidor si los datos contienen caracteres extendidos y los dos equipos tienen páginas de códigos diferentes. Los datos se interpretarán del mismo modo si ambos equipos tienen la misma página de códigos.  
  
 Cuando autotranslate está establecido en "Yes", el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client utiliza Unicode para convertir los datos que se han desplazado entre SQL_C_CHAR variables del cliente y las columnas, variables o parámetros **Char**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **VARCHAR**o **Text** de una base de datos:  
  
-   Cuando los datos se envían desde una variable de SQL_C_CHAR en el cliente a una columna, variable o parámetro de tipo **Char**, **VARCHAR**o **Text** en una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos, el controlador ODBC convierte primero de SQL_C_CHAR a Unicode mediante la ACP del cliente y, a continuación, desde Unicode a carácter mediante la ACP del servidor.  
  
-   Cuando se envían datos de una columna, una variable o un parámetro de tipo **Char**, **VARCHAR**o **Text** en una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos a una variable SQL_C_CHAR en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el cliente, el controlador ODBC de Native Client convierte primero de carácter a Unicode mediante la ACP del servidor y, a continuación, de Unicode a SQL_C_CHAR mediante la ACP del cliente.  
  
 Dado que todas estas conversiones se realizan mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client que se ejecuta en el cliente, el servidor ACP debe ser una de las páginas de códigos instaladas en el equipo cliente.  
  
 Al realizar las conversiones de caracteres mediante Unicode, se asegura la conversión correcta de todos los caracteres que existen en ambas páginas de códigos. Si un carácter existe en una página de códigos pero no en otra, el carácter no se podrá representar en la página de códigos de destino. Por ejemplo, la página de códigos 1252 tiene el símbolo de marca registrada (??), mientras que la página de códigos 437 no.  
  
 El valor AutoTranslate no tiene ningún efecto en estas conversiones:  
  
-   Mover datos entre los caracteres SQL_C_CHAR variables de cliente y las columnas, variables o parámetros Unicode **nchar**, **nvarchar**o **ntext** de las bases de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos.  
  
-   Mover datos entre las variables de cliente Unicode SQL_C_WCHAR y las **columnas, variables**o parámetros de carácter, **VARCHAR**o **Text** en las bases de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] datos.  
  
 Los datos siempre se deben convertir cuando se pasan de caracteres a Unicode.  
  
## <a name="see-also"></a>Consulte también  
 [Procesar los resultados &#40;ODBC&#41;](processing-results-odbc.md)   
 [Compatibilidad con la intercalación y Unicode](../collations/collation-and-unicode-support.md)  
  
  
