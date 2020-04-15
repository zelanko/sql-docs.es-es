---
title: Cambios de comportamiento ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e4a433531d90eb0f89d9a5e446464b13fd02526
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283445"
---
# <a name="behavioral-changes"></a>Cambios de comportamiento
Los cambios de comportamiento son aquellos cambios para los que la *sintaxis* de la interfaz sigue siendo la misma, pero la *semántica* ha cambiado. Para estos cambios, la funcionalidad utilizada en ODBC 2. *x* se comporta de forma diferente que la misma funcionalidad en ODBC 3. *x*.  
  
 Si una aplicación exhibe ODBC 2. *x* comportamiento o ODBC 3. *x* el comportamiento viene determinado por el atributo de entorno SQL_ATTR_ODBC_VERSION. Este valor de 32 bits se establece en SQL_OV_ODBC2 para exhibir ODBC 2. *x* comportamiento y SQL_OV_ODBC3 para exhibir ODBC 3. *x* comportamiento.  
  
 El atributo de entorno SQL_ATTR_ODBC_VERSION se establece mediante una llamada a **SQLSetEnvAttr**. Después de que una aplicación llama a **SQLAllocHandle** para asignar un identificador de entorno, debe llamar a**SQLSetEnvAttr** inmediatamente para establecer el comportamiento que muestra. (Como resultado, hay un nuevo estado de entorno para describir el identificador de entorno en un estado asignado, pero sin versión.) Para obtener más información, vea [Apéndice B: Tablas](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)de transición de estado ODBC .  
  
 Una aplicación indica qué comportamiento muestra con el atributo de entorno SQL_ATTR_ODBC_VERSION, pero el atributo no tiene ningún efecto en la conexión de la aplicación con un ODBC 2. *x* u ODBC 3. *x* conductor. Un ODBC 3. *x* aplicación puede conectarse a un ODBC 2. *x* o 3. *x* driver, no importa cuál sea la configuración del atributo environment.  
  
 ODBC 3. *x* las aplicaciones nunca deben llamar a **SQLAllocEnv**. Como resultado, si el Administrador de controladores recibe una llamada a **SQLAllocEnv**, reconoce la aplicación como ODBC 2. *x* aplicación.  
  
 El atributo SQL_ATTR_ODBC_VERSION afecta a tres aspectos diferentes de un ODBC 3. *x* comportamiento del conductor:  
  
-   SQLSTATE  
  
-   Tipos de datos para fecha, hora y marca de tiempo  
  
-   El *CatalogName* argumento en **SQLTables** acepta patrones de búsqueda en ODBC 3. *x*, pero no en ODBC 2. *x*  
  
 La configuración del atributo de entorno SQL_ATTR_ODBC_VERSION no afecta a **SQLSetParam** o **SQLBindParam**. **SQLColAttribute tampoco** se ve afectado por este bit. Aunque **SQLColAttribute** devuelve atributos que se ven afectados por la versión de ODBC (tipo de fecha, precisión, escala y longitud), el comportamiento previsto viene determinado por el valor de la *FieldIdentifier* argumento. Cuando *FieldIdentifier* es igual a SQL_DESC_TYPE, **SQLColAttribute** devuelve el ODBC 3. *x* códigos para la fecha, hora y marca de tiempo; cuando *FieldIdentifier* es igual a SQL_COLUMN_TYPE, **SQLColAttribute** devuelve ODBC 2. *x* códigos para la fecha, hora y marca de tiempo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Asignaciones SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Cambia el tipo de datos de fecha y hora](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
