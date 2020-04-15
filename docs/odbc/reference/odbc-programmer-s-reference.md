---
title: Programador ODBC&#39;s Referencia ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a9ca32627b9703465dcfca554fdc32ae01442e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280515"
---
# <a name="odbc-programmer39s-reference"></a>ODBC Programmer&#39;s Referencia
Referencia *del programador ODBC* contiene las secciones siguientes.  
  
-   [Novedades de ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) enumera las nuevas características ODBC que se agregaron en el SDK de Windows 8.  
  
-   [Programa ODBC](../../odbc/reference/sample-odbc-program.md) de ejemplo presenta un programa ODBC de ejemplo.  
  
-   [Introducción a ODBC](../../odbc/reference/introduction-to-odbc.md) proporciona un breve historial de lenguaje de consulta estructurado y ODBC, e información conceptual sobre la interfaz ODBC.  
  
-   [El desarrollo de aplicaciones](../../odbc/reference/develop-app/developing-applications.md) contiene información sobre el desarrollo de aplicaciones que usan la interfaz ODBC y los controladores que la implementan.  
  
-   [Instalar y configurar](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) el software ODBC proporciona información sobre la instalación y una referencia de función DLL de instalación.  
  
-   [El desarrollo de un controlador ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contiene información sobre cómo escribir un controlador.  
  
-   [Referencia de API](../../odbc/reference/syntax/odbc-reference.md) contiene sintaxis e información semántica para todas las funciones ODBC.  
  
-   [Apéndices ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contienen detalles técnicos y tablas de referencia para códigos de error ODBC, tipos de datos y gramática SQL.  
  
## <a name="working-with-the-odbc-documentation"></a>Trabajar con la documentación ODBC  
 La interfaz ODBC está diseñada para su uso con el lenguaje de programación C. El uso de la interfaz ODBC abarca tres áreas: instrucciones SQL, llamadas a funciones de ODBC y programación de C. Esta documentación supone lo siguiente:  
  
-   Un conocimiento práctico del lenguaje de programación C.  
  
-   Conocimiento general de DBMS y familiaridad con SQL.  
  
 Se utilizan las siguientes convenciones tipográficas.  
  
|Formato|Se usa para|  
|------------|--------------|  
|SELECCIONAR * DE|Las letras mayúsculas indican instrucciones SQL, nombres de macro y términos utilizados en el nivel de comando del sistema operativo.|  
|`RETCODE SQLFetch(hdbc)`|La fuente monoespacio se utiliza para líneas de comandos de ejemplo y código de programa.|  
|*Argumento*|Las palabras en cursiva indican argumentos mediante programación, información que el usuario o la aplicación debe proporcionar o énfasis de palabra.|  
|**SQLEndTran**|El tipo negrita indica que la sintaxis debe escribirse exactamente como se muestra, incluidos los nombres de función.|  
|&#124;|Una barra vertical separa dos opciones mutuamente excluyentes en una línea de sintaxis.|  
|...|Los puntos suspensivos indican que los argumentos se pueden repetir varias veces.|  
|. . .|Una columna de tres puntos indica la continuación de las líneas de código anteriores.|  
  
## <a name="about-the-code-examples"></a>Acerca de los ejemplos de código  
 Los ejemplos de código de esta guía están diseñados únicamente para fines ilustrativos. Debido a que se escriben principalmente para demostrar los principios ODBC, la eficiencia a veces se ha reservado en aras de la claridad. Además, a veces se han omitido secciones enteras de código para mayor claridad. Estas incluyen las definiciones de funciones que no son ODBC (aquellas funciones cuyos nombres no comienzan con "SQL") y la mayoría del control de errores.  
  
 Todos los ejemplos de código utilizan cadenas ANSI y el mismo esquema de base de datos, que se muestra al principio de [Funciones](../../odbc/reference/develop-app/catalog-functions.md)de catálogo .  
  
## <a name="recommended-reading"></a>Lecturas recomendadas  
 Para obtener más información acerca de SQL, están disponibles los siguientes estándares:  
  
-   Lenguaje de base de datos - SQL con mejora de integridad, ANSI, 1989 ANSI X3.135-1989.  
  
-   Idioma de la base de datos - SQL: ANSI X3H2 e ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Grupo abierto, Administración de datos: Lenguaje de consulta estructurado (SQL), versión 2 (El grupo abierto, 1996).  
  
 Además de los estándares y las guías SQL específicas del proveedor, muchos libros describen SQL, entre ellos:  
  
-   Date, C. J., con Darwen, Hugh: *A Guide to the SQL Standard* (Addison-Wesley, 1993).  
  
-   Emerson, Sandra L., Darnovsky, Marcy y Bowman, Judith S.: *The Practical SQL Handbook* (Addison-Wesley, 1989).  
  
-   Groff, James R. y Weinberg, Paul N.: *Using SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *Understanding SQL* (Sybex, 1990).  
  
-   Hursch, Jack L. y Carolyn J.: *SQL, The Structured Query Language* (TAB Books, 1988).  
  
-   Melton, Jim y Simon, Alan R.: *Understanding the New SQL: A Complete Guide* (Morgan Kaufmann Publishers, 1993).  
  
-   Pascal, Fabian: *SQL and Relational Basics* (M & T Books, 1990).  
  
-   Trimble, J. Harvey, Jr. y Chappell, David: *A Visual Introduction to SQL* (Wiley, 1989).  
  
-   Van der Lans, Rick F.: *Introducción a SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: Bases de *datos SQL y relacionales* (Microtrend Books, 1990).  
  
-   Viescas, John: Guía de *referencia rápida para SQL* (Microsoft Corp., 1989).  
  
 Para obtener información adicional sobre el procesamiento de transacciones, consulte:  
  
-   Gray, J.N. y Reuter, Andreas: *Transaction Processing: Concepts and Techniques* (Morgan Kaufmann Publishers, 1993).  
  
-   Hackathorn, Richard D.: *Enterprise Database Connectivity* (Wiley & Sons, 1993).  
  
 Para obtener más información acerca de las interfaces de nivel de llamada, están disponibles los siguientes estándares:  
  
-   Grupo abierto, Administración de datos: Interfaz de nivel de *llamada SQL (CLI), C451* (grupo abierto, 1995).  
  
-   ISO/IEC 9075-3:1995, interfaz de nivel de llamada (SQL/CLI).  
  
 Para obtener información adicional acerca de ODBC, hay varios libros disponibles, entre ellos:  
  
-   Geiger, Kyle: *Inside ODBC* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, Shoemaker, Andrew, Cross, Jim y Lilley, Albert W.: *Using ODBC 2* (Que, 1994).  
  
-   Johnston, Tom y Osborne, Mark: *ODBC Developers Guide* (Howard W. Sams & Company, 1994).  
  
-   North, Ken: Programación multiDBMS de Windows: Uso de *C++, Visual Basic, ODBC, OLE 2 y Herramientas para proyectos DBMS* (John Wiley & Sons, Inc., 1995).  
  
-   Stegman, Michael O., Signore, Robert y Creamer, John: *The ODBC Solution, Open Database Connectivity in Distributed Environments* (McGraw-Hill, 1995).  
  
-   Welch, Keith: Uso de *ODBC 2* (Que, 1994).  
  
-   Whiting, Bill: *Enséñate ODBC en veintiún días* (Howard W. Sams & Company, 1994).
