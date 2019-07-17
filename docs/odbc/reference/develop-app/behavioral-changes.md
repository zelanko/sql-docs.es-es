---
title: Cambios de comportamiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], behavioral changes
- behavioral changes [ODBC]
- compatibility [ODBC], behavioral changes
ms.assetid: a17ae701-6ab6-4eaf-9e46-d3b9cd0a3a67
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fc9f8dcc3782204c8bf1c9add1200e451edcf127
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68103873"
---
# <a name="behavioral-changes"></a>Cambios de comportamiento
Cambios de comportamiento son esos cambios para que la *sintaxis* de la interfaz sigue siendo el mismo, pero la *semántica* han cambiado. Para que estos cambios, la funcionalidad que se usa en ODBC 2. *x* se comporta de forma diferente a la misma funcionalidad en ODBC 3. *x*.  
  
 Si una aplicación exhibe ODBC 2. *x* comportamiento u ODBC 3. *x* comportamiento viene determinado por el atributo de entorno SQL_ATTR_ODBC_VERSION. Este valor de 32 bits se establece en SQL_OV_ODBC2 exhibiendo ODBC 2. *x* comportamiento y SQL_OV_ODBC3 exhibiendo ODBC 3. *x* comportamiento.  
  
 El atributo de entorno SQL_ATTR_ODBC_VERSION se establece mediante una llamada a **SQLSetEnvAttr**. Después de una aplicación llama a **SQLAllocHandle** para asignar un identificador de entorno, debe llamar a**SQLSetEnvAttr** inmediatamente para establecer el comportamiento que presenta. (Como resultado, hay un nuevo estado de entorno para describir el identificador del entorno en asignada, pero sin versión, estado). Para obtener más información, consulte [Apéndice B: Las tablas de transición de estado de ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Una aplicación indica qué comportamiento que se presenta con el atributo de entorno SQL_ATTR_ODBC_VERSION, pero el atributo no tiene ningún efecto en la conexión de la aplicación con un ODBC 2. *x* u ODBC 3. *x* controlador. Un ODBC 3. *x* aplicación puede conectarse a cualquiera un ODBC 2. *x* o 3. *x* controlador, independientemente de la configuración del atributo de entorno.  
  
 ODBC 3. *x* aplicaciones nunca deberían llamar a **SQLAllocEnv**. Como resultado, si el Administrador de controladores recibe una llamada a **SQLAllocEnv**, reconoce la aplicación como un ODBC 2. *x* aplicación.  
  
 El atributo SQL_ATTR_ODBC_VERSION afecta a tres aspectos diferentes de una aplicación ODBC 3. *x* comportamiento del controlador:  
  
-   SQLSTATE  
  
-   Tipos de datos de fecha, hora y marca de tiempo  
  
-   El *CatalogName* argumento en **SQLTables** acepta patrones de búsqueda en ODBC 3. *x*, pero no en ODBC 2. *x*  
  
 No afecta la configuración del atributo entorno SQL_ATTR_ODBC_VERSION **SQLSetParam** o **SQLBindParam**. **SQLColAttribute** también no se ve afectada por este bit. Aunque **SQLColAttribute** devuelve los atributos que se ven afectados por la versión de ODBC (tipo de fecha, precisión, escala y longitud), el comportamiento previsto viene determinada por el valor de la *FieldIdentifier*argumento. Cuando *FieldIdentifier* es igual a SQL_DESC_TYPE, **SQLColAttribute** devuelve el ODBC 3. *x* códigos para fecha, hora y marca de tiempo; cuando *FieldIdentifier* es igual a SQL_COLUMN_TYPE, **SQLColAttribute** devuelve el 2 de ODBC. *x* códigos para fecha, hora y marca de tiempo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Asignaciones SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Cambia el tipo de datos de fecha y hora](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
