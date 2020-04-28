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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e4a433531d90eb0f89d9a5e446464b13fd02526
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283445"
---
# <a name="behavioral-changes"></a>Cambios de comportamiento
Los cambios de comportamiento son los cambios para los que la *Sintaxis* de la interfaz sigue siendo la misma, pero la *semántica* ha cambiado. Para estos cambios, la funcionalidad que se usa en ODBC 2. *x* se comporta de forma diferente a la misma funcionalidad en ODBC 3. *x*.  
  
 Si una aplicación exhibe ODBC 2. comportamiento *x* u ODBC 3. el comportamiento de *x* está determinado por el atributo de entorno SQL_ATTR_ODBC_VERSION. Este valor de 32 bits se establece en SQL_OV_ODBC2 para mostrar ODBC 2. *x* y SQL_OV_ODBC3 para mostrar ODBC 3. comportamiento de *x* .  
  
 El atributo de entorno SQL_ATTR_ODBC_VERSION se establece mediante una llamada a **SQLSetEnvAttr**. Después de que una aplicación llama a **SQLAllocHandle** para asignar un identificador de entorno, debe llamar a**SQLSetEnvAttr** inmediatamente para establecer el comportamiento que exhibe. (Como resultado, hay un nuevo estado de entorno para describir el identificador de entorno en un estado asignado, pero sin versión). Para obtener más información, vea el [Apéndice B: tablas de transición de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Una aplicación indica qué comportamiento exhibe con el atributo de entorno SQL_ATTR_ODBC_VERSION, pero el atributo no tiene ningún efecto en la conexión de la aplicación con ODBC 2. *x* o ODBC 3. controlador *x* . ODBC 3. la aplicación *x* puede conectarse a ODBC 2. *x* o 3. controlador *x* , con independencia de cuál sea la configuración del atributo de entorno.  
  
 ODBC 3. las aplicaciones *x* nunca deben llamar a **SQLAllocEnv**. Como resultado, si el administrador de controladores recibe una llamada a **SQLAllocEnv**, reconoce la aplicación como ODBC 2. aplicación *x* .  
  
 El atributo SQL_ATTR_ODBC_VERSION afecta a tres aspectos diferentes de ODBC 3. comportamiento del controlador *x* :  
  
-   SQLSTATE  
  
-   Tipos de datos de fecha, hora y marca de tiempo  
  
-   El argumento *nombrecatálogo* en **SQLTables** acepta patrones de búsqueda en ODBC 3. *x*, pero no en ODBC 2. *x*  
  
 La configuración del atributo de entorno SQL_ATTR_ODBC_VERSION no afecta a **SQLSetParam** o **SQLBindParam**. **SQLColAttribute** tampoco se ve afectado por este bit. Aunque **SQLColAttribute** devuelve atributos que se ven afectados por la versión de ODBC (tipo de fecha, precisión, escala y longitud), el comportamiento previsto viene determinado por el valor del argumento *FieldIdentifier* . Cuando *FieldIdentifier* es igual a SQL_DESC_TYPE, **SQLColAttribute** devuelve ODBC 3. códigos *x* para fecha, hora y marca de tiempo; Cuando *FieldIdentifier* es igual a SQL_COLUMN_TYPE, **SQLColAttribute** devuelve ODBC 2. códigos *x* para fecha, hora y marca de tiempo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Asignaciones SQLSTATE](../../../odbc/reference/develop-app/sqlstate-mappings.md)  
  
-   [Cambia el tipo de datos de fecha y hora](../../../odbc/reference/develop-app/datetime-data-type-changes.md)
