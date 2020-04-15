---
title: Datos Unicode ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73ea9035b05f04fec1527ca2aa98531a807db8cf
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307402"
---
# <a name="unicode-data"></a>Datos Unicode
Los tipos de datos Unicode de SQL se proporcionan para describir los datos que residen en Unicode de forma nativa en el DBMS. Se proporciona un tipo de datos Unicode de C para permitir que una aplicación enlace datos a un búfer Unicode. El Administrador de controladores puede convertir datos de un tipo Unicode C (SQL_C_WCHAR) para que funcione con un controlador ANSI.  
  
 Un ODBC 3.0 o 2. *x* aplicación siempre se enlazará a los tipos de datos ANSI. Para obtener un rendimiento óptimo, una aplicación ODBC 3.5 (o superior) debe enlazarse al tipo de datos ANSI C si el tipo de columna SQL es ANSI y debe enlazarse al tipo de datos Unicode C si el tipo de columna SQL es Unicode.  
  
 Los indicadores de tipo Unicode de SQL son SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR. SQL_WCHAR datos tiene una longitud de cadena fija, mientras que SQL_WVARCHAR tiene una longitud variable con un máximo declarado y SQL_WLONGVARCHAR tiene una longitud variable con un máximo que depende del origen de datos.  
  
 El indicador de tipo Unicode c está SQL_C_WCHAR. Este es el valor predeterminado para cada uno de los indicadores de tipo Unicode de SQL. Todos los tipos SQL se pueden convertir en SQL_C_WCHAR y SQL_C_WCHAR se pueden convertir a todos los tipos SQL. Una aplicación puede recuperar datos de una de estas tres maneras:  
  
-   Recupere los datos como SQL_C_CHAR.  
  
-   Recupere los datos según SQL_C_WCHAR.  
  
-   Declare los datos como SQL_C_TCHAR. Se trata de una macro que inserta SQL_C_WCHAR si la aplicación se compila como una aplicación Unicode o inserta SQL_C_CHAR si se compila como una aplicación ANSI.  
  
 SQL_C_TCHAR se declara en una función de la siguiente manera:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Cuando la aplicación se compila como una aplicación Unicode, el *ValueType* argumento se cambiaría de SQL_C_TCHAR a SQL_C_WCHAR. Cuando la aplicación se compila como una aplicación ANSI, el *ValueType* argumento se cambiaría a SQL_C_CHAR.  
  
 Los controladores Unicode todavía deben admitir tipos de datos ANSI, incluidos SQL_CHAR. Si una aplicación que trabaja con un controlador Unicode se enlaza a SQL_CHAR, el Administrador de controladores no asignará los datos de SQL_CHAR a SQL_WCHAR. El controlador Unicode debe aceptar los datos SQL_CHAR.  
  
 El Administrador de controladores almacena los nombres de controlador y DSN en Unicode y los asigna a ANSI según sea necesario. Si un carácter Unicode no se puede asignar a un carácter ANSI (como puede ocurrir si los caracteres de una página de códigos que no es la página de códigos nativa del equipo se utilizan en los nombres de controlador y DSN), los caracteres que no se pueden convertir se representan mediante un carácter predeterminado proporcionado por el sistema.
