---
title: Programador de ODBC&#39;referencia s | Documentos de Microsoft
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
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b570b616ee14b8fd1f70b755a134be72045b1114
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-programmer39s-reference"></a>Programador de ODBC&#39;referencia s
El *referencia del programador de ODBC* contiene las siguientes secciones.  
  
-   [What's New en ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) enumera las características nuevas de ODBC que se agregaron en el SDK de Windows 8.  
  
-   [Ejemplo de programa ODBC](../../odbc/reference/sample-odbc-program.md) presenta un ejemplo de programa ODBC.  
  
-   [Introducción a ODBC](../../odbc/reference/introduction-to-odbc.md) proporciona una breve historia de lenguaje de consulta estructurado y ODBC e información conceptual acerca de la interfaz ODBC.  
  
-   [Desarrollo de aplicaciones](../../odbc/reference/develop-app/developing-applications.md) contiene información sobre cómo desarrollar aplicaciones que utilizan la interfaz ODBC y controladores que lo implementan.  
  
-   [Instalación y configuración Software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) proporciona información sobre una referencia de funciones DLL de la instalación y configuración.  
  
-   [Desarrollar un controlador ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contiene información sobre cómo escribir un controlador.  
  
-   [Referencia de la API](../../odbc/reference/syntax/odbc-reference.md) contiene información de sintaxis y semántica para todas las funciones ODBC.  
  
-   [Los apéndices ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contienen detalles técnicos y hacer referencia a tablas de gramática de SQL, tipos de datos y códigos de error ODBC.  
  
## <a name="working-with-the-odbc-documentation"></a>Trabajar con la documentación de ODBC  
 La interfaz ODBC está diseñada para su uso con el lenguaje de programación de C. Uso de la interfaz ODBC abarca tres áreas: instrucciones SQL, ODBC llamadas a funciones y programación de C. Esta documentación supone lo siguiente:  
  
-   Un conocimiento práctico del lenguaje de programación C.  
  
-   El conocimiento general DBMS y estar familiarizado con SQL.  
  
 Se utilizan las siguientes convenciones tipográficas.  
  
|Formato|Se usa para|  
|------------|--------------|  
|SELECCIONE * DE|Las letras mayúsculas indican las instrucciones SQL, nombres de macro y términos usados en el nivel de comando del sistema operativo.|  
|`RETCODE SQLFetch(hdbc)`|Se utiliza la fuente monoespaciada para líneas de comandos de ejemplo y el código de programa.|  
|*argument*|Las palabras en cursiva indican argumentos mediante programación, información que el usuario o la aplicación debe proporcionar o énfasis de word.|  
|**SQLEndTran**|Tipos en negrita indican que sintaxis debe escribirse exactamente como se muestra, incluidos los nombres de función.|  
|&#124;|Una barra vertical separa dos opciones mutuamente excluyentes en una línea de sintaxis.|  
|...|Los puntos suspensivos indican que los argumentos se pueden repetir varias veces.|  
|. . .|Una columna de tres puntos que indica que la continuación de líneas de código anteriores.|  
  
## <a name="about-the-code-examples"></a>Acerca de los ejemplos de código  
 Los ejemplos de código en esta guía están diseñados para fines informativos. Ya que está escrita principalmente para demostrar los principios ODBC, a veces se ha establecido un lado eficacia en aras de una mayor claridad. Además, en ocasiones, se han omitido secciones completas del código para mayor claridad. Esto incluye las definiciones de funciones de ODBC no (esas funciones cuyos nombres no empiezan por "SQL") y la mayoría de control de errores.  
  
 Todos los ejemplos de código utilizan cadenas ANSI y el mismo esquema de base de datos, que se muestra en el inicio de [funciones de catálogo](../../odbc/reference/develop-app/catalog-functions.md).  
  
## <a name="recommended-reading"></a>Lecturas recomendadas  
 Para obtener más información acerca de SQL, están disponibles los siguientes estándares:  
  
-   Lenguaje de base de datos: SQL con integridad mejora, ANSI, ANSI 1989 X3.135-1989.  
  
-   Lenguaje de base de datos: SQL: X3H2 ANSI e ISO/IEC 9075:1992 JTC1/SC21/WG3 (SQL-92).  
  
-   Open Group, administración de datos: Lenguaje de consulta estructurado (SQL), versión 2 (The Open Group, 1996).  
  
 Además de los estándares y las guías SQL específica del proveedor, describen muchos libros SQL, incluidas:  
  
-   Fecha, J. C., con Darwen, Hugh: *una guía para el estándar SQL* (Addison-Wesley, 1993).  
  
-   Emerson, L. Sandra, Darnovsky, María y Bowman, Judith S.: *el manual de SQL práctico* (Addison-Wesley, 1989).  
  
-   Groff, R. James y Weinberg, Paul N.: *mediante SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *descripción SQL* (Sybex, 1990).  
  
-   Hursch, L. de conector y J. Carolina: *SQL, el lenguaje de consulta estructurado* (PESTAÑA libros, 1988).  
  
-   Melton, Jim y Simon, R. Alan: *descripción el nuevo SQL: una guía completa* (Morgan Kaufmann Publishers, 1993).  
  
-   Pascal, Fabian: *SQL y conceptos básicos relacional* (M & T libros, 1990).  
  
-   Trimble, Harvey J., Jr. y Chappell, David: *una presentación Visual SQL* (Wiley, 1989).  
  
-   Van der LAN, Rick F.: *Introducción a SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL y bases de datos relacionales* (Microtrend libros, 1990).  
  
-   Viescas, Juan: *Guía de referencia rápida para SQL* (Microsoft Corp., 1989).  
  
 Para obtener información adicional sobre el procesamiento de transacciones, vea:  
  
-   Gris, N. J. y Reuter, Andreas: *el procesamiento de transacciones: conceptos y técnicas* (Morgan Kaufmann Publishers, 1993).  
  
-   Hackathorn, Richard D.: *conectividad de bases de datos de empresa* (Wiley & hijos, 1993).  
  
 Para obtener más información sobre las Interfaces de nivel de llamada, están disponibles los siguientes estándares:  
  
-   Open Group *administración de datos: SQL llamada nivel interfaz (CLI), C451* (Open Group-1995).  
  
-   ISO/IEC 9075-3:1995, interfaz de nivel de llamada (SQL/CLI).  
  
 Para obtener información adicional acerca de ODBC, un número de libros está disponible, incluyendo:  
  
-   Geiger, Kyle: *dentro de ODBC* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, zapateros, Andrew, cruz, Jim y Lilley, W. Albert: *mediante ODBC 2* (Que, 1994).  
  
-   Johnston, Tom y Osborne, marca: *guía para desarrolladores de ODBC* (Howard W. Sams & empresa, 1994).  
  
-   Norte, Ken: *Windows Multi-DBMS programación: uso de C++, Visual Basic, ODBC, OLE 2 y herramientas para proyectos DBMS* (John Wiley & hijos, Inc., 1995).  
  
-   Stegman, Michael o, Signore, Robert y crema, Juan: *la solución ODBC, conectividad abierta de base de datos en entornos distribuidos* (McGraw-Hill, 1995).  
  
-   Welch, Keith: *mediante ODBC 2* (Que, 1994).  
  
-   Merlán, Bill: *enseñar ODBC en 21 días* (Howard W. Sams & empresa, 1994).
