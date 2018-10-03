---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74de6c44aaf109a434f0cf76c6902abfba92efe1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47655023"
---
# <a name="unicode-data"></a>Datos Unicode
Tipos de datos Unicode de SQL se proporcionan para describir los datos que residen en Unicode de forma nativa en el DBMS. Un tipo de datos Unicode C se proporciona para permitir que una aplicación enlazar datos a un búfer de Unicode. El Administrador de controladores puede convertir los datos de un tipo de C de Unicode (SQL_C_WCHAR) para que sea la función con un controlador de ANSI.  
  
 Un ODBC 3.0 o 2. *x* aplicación siempre se enlazará a los tipos de datos ANSI. Para un rendimiento óptimo, una aplicación de ODBC 3.5 (o posterior) debe enlazar al tipo de datos C ANSI si el tipo de columna SQL es ANSI y debe enlazarse con el tipo de datos Unicode C si el tipo de columna SQL es Unicode.  
  
 Los indicadores de tipo Unicode de SQL son SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR. Datos SQL_WCHAR tienen una longitud de cadena fija mientras SQL_WVARCHAR tiene una longitud variable con un máximo declarado y SQL_WLONGVARCHAR tiene una longitud variable con un máximo que depende del origen de datos.  
  
 El indicador de tipo Unicode C es SQL_C_WCHAR. Este es el valor predeterminado para cada uno de los indicadores de tipo Unicode de SQL. Todos los tipos SQL pueden convertirse en SQL_C_WCHAR, y SQL_C_WCHAR puede convertirse en todos los tipos SQL. Una aplicación puede recuperar datos en una de estas tres maneras:  
  
-   Recuperar los datos como SQL_C_CHAR.  
  
-   Recuperar los datos como SQL_C_WCHAR.  
  
-   Declare los datos como SQL_C_TCHAR. Se trata de una macro que inserta SQL_C_WCHAR si la aplicación se compila como una aplicación Unicode o inserta SQL_C_CHAR si se ha compilado como una aplicación de ANSI.  
  
 SQL_C_TCHAR se declara en una función como sigue:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Cuando se compila la aplicación como una aplicación de Unicode, el *ValueType* argumento SQL_C_TCHAR se cambiaría a SQL_C_WCHAR. Cuando se compila la aplicación como una aplicación ANSI, el *ValueType* argumento cambiaría a SQL_C_CHAR.  
  
 Controladores de Unicode aún deben admitir los tipos de datos de ANSI, incluidos SQL_CHAR. Si una aplicación trabaja con un controlador de Unicode se enlaza a SQL_CHAR, el Administrador de controladores no asigna los datos SQL_CHAR a SQL_WCHAR. El controlador de Unicode debe aceptar los datos SQL_CHAR.  
  
 El Administrador de controladores almacena los controladores y los nombres DSN en Unicode y los asigna a ANSI según sea necesario. Si un carácter Unicode no se puede asignar a un carácter ANSI (ya que puede ocurrir si se utilizan caracteres de una página de códigos que no es la página de código nativo del equipo en el controlador y los nombres de los DSN), los caracteres que no se podrían convertir se representan mediante un sup de carácter predeterminado plied por el sistema.
