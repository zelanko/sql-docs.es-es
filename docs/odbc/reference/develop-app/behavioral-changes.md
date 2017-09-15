---
title: Cambios de comportamiento | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5709d3ef8d186d0dcc0fb56f27829298f74e2b0c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="behavioral-changes"></a>Cambios de comportamiento
Cambios de comportamiento son esos cambios para que la *sintaxis* de la interfaz sigue siendo el mismo, pero la *semántica* han cambiado. Para que estos cambios, la funcionalidad que se usa en ODBC 2. *x* se comporta de forma diferente a la misma funcionalidad en ODBC 3.* x*.  
  
 Si una aplicación exhibe ODBC 2. *x* comportamiento u ODBC 3.* x* comportamiento viene determinado por el atributo de entorno SQL_ATTR_ODBC_VERSION. Este valor de 32 bits se establece en SQL_OV_ODBC2 exhiba ODBC 2. *x* comportamiento y SQL_OV_ODBC3 exhiba ODBC 3.* x* comportamiento.  
  
 El atributo de entorno SQL_ATTR_ODBC_VERSION se establece mediante una llamada a **SQLSetEnvAttr**. Después de que una aplicación llama **SQLAllocHandle** para asignar un identificador de entorno, debe llamar a**SQLSetEnvAttr** inmediatamente para establecer el comportamiento exhibe. (Como resultado, hay un nuevo estado de entorno para describir el identificador de entorno en un asignado, pero sin versión, estado). Para obtener más información, consulte [tablas de transición de estado de apéndice B: ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Una aplicación indica qué comportamiento exhibe con el atributo de entorno SQL_ATTR_ODBC_VERSION, pero el atributo no tiene ningún efecto en la conexión de la aplicación con una API ODBC 2. *x* u ODBC 3.* x* controlador. Un ODBC 3. *x* aplicación puede conectarse a cualquiera una API ODBC 2.* x* o 3.* x* controlador, con independencia de la configuración del atributo de entorno.  
  
 ODBC 3. *x* nunca deben llamar las aplicaciones **SQLAllocEnv**. Como resultado, si el Administrador de controladores recibe una llamada a **SQLAllocEnv**, reconoce la aplicación como una API ODBC 2.* x* aplicación.  
  
 El atributo SQL_ATTR_ODBC_VERSION afecta a tres aspectos diferentes de una aplicación ODBC 3. *x* comportamiento del controlador:  
  
-   SQLSTATE  
  
-   Tipos de datos de fecha, hora y marca de tiempo  
  
-   El *CatalogName* argumento en **SQLTables** acepta patrones de búsqueda en ODBC 3.* x*, pero no en ODBC 2.* x*  
  
 No afecta la configuración del atributo de entorno SQL_ATTR_ODBC_VERSION **SQLSetParam** o **SQLBindParam**. **SQLColAttribute** también no se ve afectada por este bit. Aunque **SQLColAttribute** devuelve atributos que se ven afectados por la versión de ODBC (tipo de fecha, precisión, escala y longitud), el comportamiento previsto viene determinado por el valor de la *FieldIdentifier*argumento. Cuando *FieldIdentifier* es igual a SQL_DESC_TYPE, **SQLColAttribute** devuelve ODBC 3.* x* códigos de fecha, hora y marca de tiempo; cuando *FieldIdentifier* es igual a SQL_COLUMN_TYPE, **SQLColAttribute** devuelve la API ODBC 2.* x* códigos de fecha, hora y marca de tiempo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Asignaciones SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Cambia el tipo de datos de fecha y hora](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
