---
title: Programador de ODBC&#39;referencia s | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c83a7de609d200da2957a65b9325d031eda49780
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273037"
---
# <a name="odbc-programmer39s-reference"></a>Programador de ODBC&#39;s referencia
El *referencia del programador de ODBC* contiene las siguientes secciones.  
  
-   [Novedades de ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) enumera las características nuevas de ODBC que se agregaron en el SDK de Windows 8.  
  
-   [Programa de ODBC de ejemplo](../../odbc/reference/sample-odbc-program.md) presenta un programa ODBC de ejemplo.  
  
-   [Introducción a ODBC](../../odbc/reference/introduction-to-odbc.md) proporciona una breve historia de lenguaje de consulta estructurado, ODBC y obtener información conceptual acerca de la interfaz ODBC.  
  
-   [Desarrollo de aplicaciones](../../odbc/reference/develop-app/developing-applications.md) contiene información sobre cómo desarrollar aplicaciones que utilizan la interfaz ODBC y controladores que lo implementan.  
  
-   [Instalación y configuración Software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) proporciona información sobre una referencia de funciones DLL de instalación y configuración.  
  
-   [Desarrollar un controlador ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contiene información sobre cómo escribir un controlador.  
  
-   [Referencia de API](../../odbc/reference/syntax/odbc-reference.md) contiene información de sintaxis y semántica para todas las funciones ODBC.  
  
-   [Apéndices ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contienen detalles técnicos y hacer referencia a tablas de la gramática de SQL, tipos de datos y códigos de error ODBC.  
  
## <a name="working-with-the-odbc-documentation"></a>Trabajar con la documentación de ODBC  
 La interfaz ODBC está diseñada para su uso con el lenguaje de programación de C. Uso de la interfaz ODBC abarca tres áreas: Las instrucciones SQL, llamadas a funciones ODBC y programación de C. Esta documentación asume lo siguiente:  
  
-   Conocimiento práctico del lenguaje de programación C.  
  
-   Conocimientos generales DBMS así como familiaridad con SQL.  
  
 Se utilizan las siguientes convenciones tipográficas.  
  
|Formato|Se usa para|  
|------------|--------------|  
|SELECCIONAR * DESDE|Letras mayúsculas indican las instrucciones SQL, los nombres de macro y términos usados en el nivel de comando del sistema operativo.|  
|`RETCODE SQLFetch(hdbc)`|Se utiliza la fuente monoespaciada para líneas de comandos de ejemplo y código de programa.|  
|*argument*|Las palabras en cursiva indican argumentos mediante programación, la información que el usuario o la aplicación debe proporcionar o énfasis en word.|  
|**SQLEndTran**|Los tipos en negrita indican la sintaxis debe escribirse exactamente como se muestra, incluidos los nombres de función.|  
|&#124;|Una barra vertical separa dos opciones mutuamente excluyentes en una línea de sintaxis.|  
|…|Los puntos suspensivos indican que los argumentos se pueden repetir varias veces.|  
|. . .|Una columna de tres puntos indica a continuación de líneas de código anteriores.|  
  
## <a name="about-the-code-examples"></a>Acerca de los ejemplos de código  
 Los ejemplos de código en esta guía están diseñados únicamente por motivos ilustrativos. Ya que está escrita principalmente para demostrar los principios ODBC, a veces se ha establecido un lado la eficacia para mayor claridad. Además, a veces se han omitido secciones completas del código para mayor claridad. Estas son las definiciones de funciones que no son ODBC (esas funciones cuyos nombres no comiencen por "SQL") y la mayoría de los errores.  
  
 Todos los ejemplos de código usan cadenas ANSI y el mismo esquema de base de datos, que se muestra al principio de [funciones de catálogo](../../odbc/reference/develop-app/catalog-functions.md).  
  
## <a name="recommended-reading"></a>Lecturas recomendadas  
 Para obtener más información acerca de SQL, están disponibles los siguientes estándares:  
  
-   SQL con integridad mejora, ANSI, 1989 ANSI X3.135-1989 - idioma de la base de datos.  
  
-   Lenguaje de base de datos: SQL: ANSI X3H2 y ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Open Group Data Management: Lenguaje de consulta estructurado (SQL), versión 2 (The Open Group, 1996).  
  
 Además de los estándares y guías de SQL específicas del proveedor, describen muchos libros SQL, incluidos:  
  
-   Fecha, J. C., con Darwen, Hugh: *Una guía para el estándar SQL* (Addison-Wesley, 1993).  
  
-   Emerson, L. Sandra, Darnovsky, María y Bowman, Judith S.: *El manual de SQL práctico* (Addison-Wesley, 1989).  
  
-   Groff, James R. and Weinberg, Paul N.: *Mediante SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *Descripción de SQL* (Sybex, 1990).  
  
-   Hursch, Jack l y J. Carolina: *SQL, el lenguaje de consulta estructurado* (PESTAÑA libros, 1988).  
  
-   Melton, Jim y Simon, R. Alan: *Cómo entender el nuevo SQL: A Complete Guide* (Morgan Kaufmann Publishers, 1993).  
  
-   Fabian de Pascal: *SQL y los conceptos básicos de relacionales* (M & T libros, 1990).  
  
-   Trimble, J. Harvey, Jr. y Chappell, David: *Una introducción Visual a SQL* (Wiley, 1989).  
  
-   LAN van der, Rick F.: *Introducción a SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL y bases de datos relacionales* (Microtrend libros, 1990).  
  
-   Viescas, John: *Guía de referencia rápida SQL* (Microsoft Corp., 1989).  
  
 Para obtener más información sobre el procesamiento de transacciones, vea:  
  
-   Gris, N. J. y Reuter, Andreas: *Procesamiento de transacciones: Conceptos y técnicas* (Morgan Kaufmann Publishers, 1993).  
  
-   Hackathorn, Richard D.: *Enterprise Database Connectivity* (Wiley & Sons, 1993).  
  
 Para obtener más información sobre las Interfaces de nivel de llamada, están disponibles los siguientes estándares:  
  
-   Open Group *administración de datos: SQL llamada nivel interfaz (CLI), C451* (Open Group, 1995).  
  
-   ISO/IEC 9075-3:1995, interfaz de nivel de llamada (SQL/CLI).  
  
 Para obtener más información acerca de ODBC, un número de los libros en pantalla está disponible, incluyendo:  
  
-   Geiger, Kyle: *Dentro de ODBC* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, Shoemaker, Andrew, Cross, Jim, and Lilley, Albert W.: *Uso de ODBC 2* (Que, 1994).  
  
-   Johnston, Tom y Osborne, marca: *Guía para desarrolladores de ODBC* (Howard W. Sams & compañía, 1994).  
  
-   Norte, Ken: *Programación de Multi-DBMS de Windows: Uso de C++, Visual Basic, ODBC, OLE 2 y herramientas para proyectos DBMS* (John Wiley & Sons, Inc., 1995).  
  
-   Stegman, O. Michael, Signore, Robert y crema, John: *La solución ODBC, conectividad abierta de base de datos en entornos distribuidos* (McGraw-Hill, 1995).  
  
-   Welch, Keith: *Uso de ODBC 2* (Que, 1994).  
  
-   Merlán, factura: *Enseñar ODBC en 21 días* (Howard W. Sams & compañía, 1994).
