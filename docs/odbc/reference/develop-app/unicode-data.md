---
title: Datos Unicode | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], data
- data types [ODBC], Unicode
- C data types [ODBC], Unicode
- SQL data types [ODBC], Unicode
ms.assetid: abc28718-e6d9-49fb-97ff-402d50c3c375
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7871576f95ebb49708036d531c4f2d8eebbac863
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="unicode-data"></a>Datos Unicode
Tipos de datos Unicode de SQL se proporcionan para describir los datos que se encuentra en formato Unicode de forma nativa en el DBMS. Un tipo de datos Unicode C se proporciona para permitir que una aplicación enlazar datos a un búfer de Unicode. El Administrador de controladores puede convertir los datos de un tipo de Unicode C (SQL_C_WCHAR) para que sea la función con un controlador de ANSI.  
  
 ODBC 3.0 o 2. *x* aplicación siempre se enlazará a los tipos de datos de ANSI. Para obtener un rendimiento óptimo, una aplicación de ODBC 3.5 (o posterior) debe enlazar al tipo de datos C ANSI si el tipo de columna SQL es ANSI y si el tipo de columna SQL es Unicode se debe enlazar al tipo de datos Unicode C.  
  
 Los indicadores de tipo Unicode SQL son SQL_WCHAR, SQL_WVARCHAR y SQL_WLONGVARCHAR. Datos SQL_WCHAR tienen una longitud de cadena fija, mientras que SQL_WVARCHAR tiene una longitud variable con un máximo declarado y SQL_WLONGVARCHAR tiene una longitud variable con un máximo que depende del origen de datos.  
  
 El indicador de tipo Unicode C es SQL_C_WCHAR. Este es el valor predeterminado para cada uno de los indicadores de tipo Unicode de SQL. Todos los tipos SQL pueden convertirse a SQL_C_WCHAR, y SQL_C_WCHAR se puede convertir a todos los tipos SQL. Una aplicación puede recuperar los datos de una de estas tres maneras:  
  
-   Recuperar los datos como SQL_C_CHAR.  
  
-   Recuperar los datos de forma que SQL_C_WCHAR.  
  
-   Declare los datos como SQL_C_TCHAR. Se trata de una macro que inserta SQL_C_WCHAR si la aplicación se compila como una aplicación Unicode o inserta SQL_C_CHAR si se ha compilado como una aplicación de ANSI.  
  
 SQL_C_TCHAR se declara en una función como sigue:  
  
```  
SQLBindParameter(StatementHandle, 1, SQL_PARAM_INPUT, SQL_C_TCHAR, SQL_WCHAR, NameLen, 0, Name, 0, &Name)  
```  
  
 Cuando se compila la aplicación como una aplicación de Unicode, la *ValueType* argumento SQL_C_TCHAR se cambiaría a SQL_C_WCHAR. Cuando se compila la aplicación como una aplicación ANSI, el *ValueType* argumento cambiaría a SQL_C_CHAR.  
  
 Controladores de Unicode aún deben admitir tipos de datos de ANSI, incluidos SQL_CHAR. Si enlaza SQL_CHAR una aplicación trabaja con un controlador de Unicode, el Administrador de controladores no se asignarán los datos SQL_CHAR a SQL_WCHAR. El controlador de Unicode debe aceptar los datos SQL_CHAR.  
  
 El Administrador de controladores se almacena los nombres DSN y el controlador en Unicode y se asignan a ANSI según sea necesario. Si un carácter Unicode no se puede asignar a un carácter ANSI (ya que puede ocurrir si se utilizan caracteres de una página de códigos que no es la página de código nativo del equipo en el controlador y los nombres de DSN), los caracteres que no se pudieron convertir se representan mediante un sup de carácter predeterminado plied por el sistema.
