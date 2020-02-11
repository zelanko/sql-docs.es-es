---
title: Referencia del programador de ODBC&#39;s | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fd729956ee7bb1fccf7a8fceb7a435042df4df7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111192"
---
# <a name="odbc-programmer39s-reference"></a>Referencia del programador de ODBC&#39;s
La *Referencia del programador de ODBC* contiene las siguientes secciones.  
  
-   [Novedades de odbc 3,8](../../odbc/reference/what-s-new-in-odbc-3-8.md) enumera las nuevas características de ODBC que se agregaron en el SDK de Windows 8.  
  
-   El [programa ODBC de ejemplo](../../odbc/reference/sample-odbc-program.md) presenta un programa ODBC de ejemplo.  
  
-   La [Introducción a ODBC](../../odbc/reference/introduction-to-odbc.md) proporciona un breve historial de lenguaje de consulta estructurado y ODBC, así como información conceptual sobre la interfaz ODBC.  
  
-   El [desarrollo de aplicaciones](../../odbc/reference/develop-app/developing-applications.md) contiene información sobre el desarrollo de aplicaciones que usan la interfaz y los controladores ODBC que la implementan.  
  
-   La instalación [y configuración del software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) proporciona información acerca de la instalación y una referencia de la función dll del programa de instalación.  
  
-   El [desarrollo de un controlador ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contiene información sobre la escritura de un controlador.  
  
-   La [referencia de API](../../odbc/reference/syntax/odbc-reference.md) contiene información sobre la sintaxis y la semántica de todas las funciones ODBC.  
  
-   Los [apéndices de ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contienen detalles técnicos y tablas de referencia para los códigos de error, los tipos de datos y la gramática de SQL de ODBC.  
  
## <a name="working-with-the-odbc-documentation"></a>Trabajar con la documentación de ODBC  
 La interfaz ODBC está diseñada para su uso con el lenguaje de programación C. El uso de la interfaz ODBC abarca tres áreas: instrucciones SQL, llamadas a funciones ODBC y programación C. En esta documentación se presupone lo siguiente:  
  
-   Conocimiento práctico del lenguaje de programación C.  
  
-   Conocimientos generales de DBMS y familiaridad con SQL.  
  
 Se utilizan las siguientes convenciones tipográficas.  
  
|Formato|Se usa para|  
|------------|--------------|  
|SELECT * FROM|Las letras mayúsculas indican instrucciones SQL, nombres de macro y términos que se usan en el nivel de comando del sistema operativo.|  
|`RETCODE SQLFetch(hdbc)`|La fuente de monoespacio se utiliza para las líneas de comandos y el código de programa de ejemplo.|  
|*argument*|Las palabras en cursiva indican argumentos de programación, información que debe proporcionar el usuario o la aplicación, o el énfasis en la palabra.|  
|**SQLEndTran**|El tipo Bold indica que la sintaxis debe escribirse exactamente como se muestra, incluidos los nombres de función.|  
|&#124;|Una barra vertical separa dos opciones mutuamente excluyentes en una línea de sintaxis.|  
|...|Un botón de puntos suspensivos indica que los argumentos se pueden repetir varias veces.|  
|. . .|Una columna de tres puntos indica la continuación de las líneas de código anteriores.|  
  
## <a name="about-the-code-examples"></a>Acerca de los ejemplos de código  
 Los ejemplos de código de esta guía se han diseñado únicamente con fines ilustrativos. Dado que se escriben principalmente para demostrar los principios de ODBC, a veces se ha reservado la eficacia en aras de la claridad. Además, a veces se han omitido secciones completas de código para mayor claridad. Entre ellas se incluyen las definiciones de funciones que no son de ODBC (las funciones cuyos nombres no comienzan por "SQL") y la mayoría del control de errores.  
  
 Todos los ejemplos de código usan cadenas ANSI y el mismo esquema de la base de datos, que se muestra al principio de [las funciones de catálogo](../../odbc/reference/develop-app/catalog-functions.md).  
  
## <a name="recommended-reading"></a>Lecturas recomendadas  
 Para obtener más información acerca de SQL, están disponibles los siguientes estándares:  
  
-   Lenguaje de base de datos: SQL con mejoras de integridad, ANSI, 1989 ANSI X 3.135-1989.  
  
-   Lenguaje de base de datos: SQL: ANSI X3H2 e ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Abrir Grupo, Administración de datos: Lenguaje de consulta estructurado (SQL), versión 2 (el grupo abierto, 1996).  
  
 Además de los estándares y las guías de SQL específicas del proveedor, muchos libros describen SQL, entre los que se incluyen:  
  
-   Date, C. J., con Darwen, Hugh: *Guía del estándar SQL* (Addison-Wesley, 1993).  
  
-   Emerson, Sandra L., Darnovsky, Marcy y Bowman, Judith S.: *el manual práctico de SQL* (Addison-Wesley, 1989).  
  
-   Groff, James R. y Weinberg, Paul N.: *uso de SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *Descripción de SQL* (Sybex, 1990).  
  
-   Hursch, Jack L. y Carolina J.: *SQL, la lenguaje de consulta estructurado* (libros de pestañas, 1988).  
  
-   Melton, Jim y Simon, Alan R.: *Descripción de la nueva guía SQL: A complete* (publicadores de Morgan Kaufmann, 1993).  
  
-   Pascal, Fabian: *aspectos básicos de SQL y relacionales* (libros M & T, 1990).  
  
-   Trimble, J. Harvey, Jr. y Chappell, David: *una introducción visual a SQL* (Wiley, 1989).  
  
-   Furgoneta der LAN, Rick F.: *Introducción a SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL y bases de datos relacionales* (libros de microtrend, 1990).  
  
-   Viescas, John: *Guía de referencia rápida de SQL* (Microsoft Corp., 1989).  
  
 Para obtener información adicional sobre el procesamiento de transacciones, vea:  
  
-   Gris, J. N. y Reuter, Andreas: *procesamiento de transacciones: conceptos y técnicas* (publicadores de Morgan Kaufmann, 1993).  
  
-   Hackathorn, Richard D.: *conectividad de base de datos empresarial* (Wiley & hijos, 1993).  
  
 Para obtener más información sobre las interfaces de nivel de llamada, hay disponibles los siguientes estándares:  
  
-   Abrir Grupo, *Administración de datos: interfaz de nivel de llamada de SQL (CLI), C451* (abrir grupo, 1995).  
  
-   ISO/IEC 9075-3:1995, interfaz de nivel de llamada (SQL/CLI).  
  
 Para obtener información adicional acerca de ODBC, hay disponibles varios libros, entre los que se incluyen:  
  
-   Geiger, Kyle: *dentro de ODBC* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, Shoemaker, Andrew, Cross, Jim y Lilley, Albert W.: *using ODBC 2* (que, 1994).  
  
-   Johnston, Tom y Osborne, Mark: *Guía para desarrolladores de ODBC* (Howard W. Sams & Company, 1994).  
  
-   Norte, Ken: *programación de varios DBMS de Windows: uso de C++, Visual Basic, ODBC, OLE 2 y herramientas para proyectos de DBMS* (John Wiley & hijos, Inc., 1995).  
  
-   Stegman, Michael O., Signore, Robert y crema, John: *la solución ODBC, Conectividad abierta de bases de datos en entornos distribuidos* (McGraw-Hill, 1995).  
  
-   Welch, Keith: *usar ODBC 2 (con* , 1994).  
  
-   Whiting, Bill: *enseñe su ODBC en un plazo de veinticinco días* (Howard W. Sams & Company, 1994).
