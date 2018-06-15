---
title: Cambios de comportamiento y los controladores ODBC 3.x | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f5eed90b0cfea267e2184018251d7a42da8bf670
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906200"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>Cambios de comportamiento y los controladores ODBC 3.x
El atributo de entorno SQL_ATTR_ODBC_VERSION indica al controlador si necesita exhiba ODBC 2. *x* comportamiento u ODBC 3 *.x* comportamiento. ¿Cómo se establece el atributo de entorno SQL_ATTR_ODBC_VERSION depende de la aplicación. ODBC 3 *.x* las aplicaciones deben llamar a **SQLSetEnvAttr** para establecer este atributo después de que llame a **SQLAllocHandle** para asignar un identificador de entorno y antes de llamar a  **SQLAllocHandle** para asignar un identificador de conexión. Si no pueden hacer esto, el Administrador de controladores devuelve SQLSTATE HY010 (error de secuencia de función) en la última llamada a **SQLAllocHandle**.  
  
> [!NOTE]  
>  Para obtener más información sobre cómo debe actuar ante una aplicación y los cambios de comportamientos, consulte [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 ODBC 2. *x* aplicaciones y ODBC 2. *x* aplicaciones vuelven a compilar con ODBC 3 *.x* archivos de encabezado no llame a **SQLSetEnvAttr**. Sin embargo, llaman a **SQLAllocEnv** en lugar de **SQLAllocHandle** para asignar un identificador de entorno. Por lo tanto, cuando la aplicación llama **SQLAllocEnv** en el Administrador de controladores, el Administrador de controladores llama **SQLAllocHandle** y **SQLSetEnvAttr** en el controlador. Por lo tanto, ODBC 3 *.x* controladores siempre pueden contar con este atributo que se va a establecer.  
  
 Si una aplicación compatible con los estándares compilado con la marca de compilación ODBC_STD llamadas **SQLAllocEnv** (que puede producirse porque **SQLAllocEnv** no está en desuso en la norma ISO), la llamada se asigna a  **SQLAllocHandleStd** en tiempo de compilación. Durante la ejecución, la aplicación llama **SQLAllocHandleStd**. El Administrador de controladores, se establece el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3. Una llamada a **SQLAllocHandleStd** equivale a una llamada a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV y una llamada a **SQLSetEnvAttr** establecer SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3.  
  
 En ciertas arquitecturas de controlador, es necesario para el controlador para que aparezca como una API ODBC 2. *x* controlador o una aplicación ODBC 3 *.x* controlador, dependiendo de la conexión. El controlador en este caso podría no ser un controlador, pero es una capa que se encuentra entre el Administrador de controladores y otro controlador. Por ejemplo, podría imitar un controlador, como ODBC Spy. En otro ejemplo, puede actuar como puerta de enlace, como EDA/SQL. Para que aparezca como una aplicación ODBC 3 *.x* controlador, este tipo de controlador debe ser capaz de exportar **SQLAllocHandle**y para que aparezca como una API ODBC 2. *x* controlador, debe ser capaz de exportar **SQLAllocConnect**, **SQLAllocEnv**, y **SQLAllocStmt**. Cuando un entorno, la conexión o la instrucción se va a asignar a, el Administrador de controladores se comprueba para ver si exporta este controlador **SQLAllocHandle**. Puesto que el controlador hace, las llamadas de administrador de controladores **SQLAllocHandle** en el controlador. Si el controlador está trabajando con una API ODBC 2. *x* controlador, el controlador debe asignar la llamada a **SQLAllocHandle** a **SQLAllocConnect**, **SQLAllocEnv**, o  **SQLAllocStmt**, según corresponda. También debe hacer nada con la **SQLSetEnvAttr** a llamar cuando se comporta como una API ODBC 2. *x* controlador.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de datos de fecha y hora](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [Compatibilidad con versiones anteriores de los tipos de datos de C](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [Marcadores de longitud fija](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [Compatibilidad con SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [Devuelve SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [Llamar a SQLSetPos para insertar datos](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [Cargar por ordinal](../../../odbc/reference/appendixes/loading-by-ordinal.md)
