---
description: Datos Unicode
title: Datos Unicode | Microsoft Docs
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
ms.openlocfilehash: f217e6b629936cc835d134c89d972bb1408b9d0b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88339121"
---
# <a name="unicode-data"></a>Datos Unicode
Los tipos de datos Unicode de SQL se proporcionan para describir los datos que residen en Unicode de forma nativa en el DBMS. Se proporciona un tipo de datos Unicode de C para permitir que una aplicación enlace datos a un búfer Unicode. El administrador de controladores puede convertir datos de un tipo C de Unicode (SQL_C_WCHAR) para que funcionen con un controlador ANSI.  
  
 ODBC 3,0 o 2. la aplicación *x* siempre se enlazará a los tipos de datos ANSI. Para obtener un rendimiento óptimo, una aplicación ODBC 3,5 (o posterior) debe enlazarse al tipo C de datos ANSI si el tipo de columna SQL es ANSI y debe enlazarse al tipo de datos C de Unicode si el tipo de columna SQL es Unicode.  
  
 Los indicadores de tipo Unicode de SQL son SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR. SQL_WCHAR datos tienen una longitud de cadena fija, mientras que SQL_WVARCHAR tiene una longitud variable con un máximo declarado y SQL_WLONGVARCHAR tiene una longitud variable con un valor máximo que depende del origen de datos.  
  
 El indicador de tipo Unicode de C está SQL_C_WCHAR. Este es el valor predeterminado para cada uno de los indicadores de tipo Unicode de SQL. Todos los tipos SQL se pueden convertir en SQL_C_WCHAR y SQL_C_WCHAR se pueden convertir en todos los tipos de SQL. Una aplicación puede recuperar datos de una de estas tres maneras:  
  
-   Recupere los datos como SQL_C_CHAR.  
  
-   Recupere los datos como SQL_C_WCHAR.  
  
-   Declare los datos como SQL_C_TCHAR. Se trata de una macro que inserta SQL_C_WCHAR si la aplicación se compila como una aplicación Unicode o inserta SQL_C_CHAR si se compila como una aplicación ANSI.  
  
 SQL_C_TCHAR se declara en una función como se indica a continuación:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Cuando la aplicación se compila como una aplicación Unicode, el argumento *ValueType* se cambiaría de SQL_C_TCHAR a SQL_C_WCHAR. Cuando la aplicación se compila como una aplicación ANSI, el argumento *ValueType* se cambiaría a SQL_C_CHAR.  
  
 Los controladores Unicode todavía deben admitir tipos de datos ANSI, incluidos SQL_CHAR. Si una aplicación que trabaja con un controlador Unicode se enlaza a SQL_CHAR, el administrador de controladores no asignará los datos de SQL_CHAR a SQL_WCHAR. El controlador Unicode debe aceptar los datos de SQL_CHAR.  
  
 El administrador de controladores almacena los nombres de controlador y DSN en Unicode y los asigna a ANSI según sea necesario. Si un carácter Unicode no se puede asignar a un carácter ANSI (como puede ocurrir si los caracteres de una página de códigos que no es la página de códigos nativa del equipo se utilizan en los nombres de controlador y DSN), los caracteres que no se pudieron convertir se representan mediante un carácter predeterminado proporcionado por el sistema.
