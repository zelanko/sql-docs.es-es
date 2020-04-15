---
title: Cambios de comportamiento y controladores ODBC 3.x Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_attr_odbc_version [ODBC]
- backward compatibility [ODBC], behavioral changes
- compatibility [ODBC], behavioral changes
ms.assetid: 88a503cc-bff7-42d9-83ff-8e232109ed06
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d8343573261d74a6a0c652cf425b12da91f7cb0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292369"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>Cambios de comportamiento y controladores ODBC 3.x
El atributo de entorno SQL_ATTR_ODBC_VERSION indica al controlador si necesita mostrar el comportamiento ODBC *2.x* o el comportamiento ODBC *3.x.* La forma en que se establece el atributo de entorno SQL_ATTR_ODBC_VERSION depende de la aplicación. Las aplicaciones ODBC *3.x* deben llamar a **SQLSetEnvAttr** para establecer este atributo después de llamar a **SQLAllocHandle** para asignar un identificador de entorno y antes de llamar a **SQLAllocHandle** para asignar un identificador de conexión. Si no lo hacen, el Administrador de controladores devuelve SQLSTATE HY010 (error de secuencia de funciones) en esta última llamada a **SQLAllocHandle**.  
  
> [!NOTE]  
>  Para obtener más información sobre los cambios de comportamiento y cómo actúa una aplicación, vea [Cambios de](../../../odbc/reference/develop-app/behavioral-changes.md)comportamiento .  
  
 Las aplicaciones ODBC *2.x* y las aplicaciones ODBC *2.x* recompiladas con los archivos de encabezado ODBC *3.x* no llaman a **SQLSetEnvAttr**. Sin embargo, llaman a **SQLAllocEnv** en lugar de **SQLAllocHandle** para asignar un identificador de entorno. Por lo tanto, cuando la aplicación llama a **SQLAllocEnv** en el Administrador de controladores, el Administrador de controladores llama **sqlAllocHandle** y **SQLSetEnvAttr** en el controlador. Por lo tanto, los controladores ODBC *3.x* siempre pueden contar con este atributo que se establece.  
  
 Si una aplicación compatible con estándares compilada con el indicador de compilación ODBC_STD llama a **SQLAllocEnv** (que puede producirse porque **SQLAllocEnv** no está en desuso en ISO), la llamada se asigna a **SQLAllocHandleStd** en tiempo de compilación. En tiempo de ejecución, la aplicación llama a **SQLAllocHandleStd**. El Administrador de controladores establece el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3. Una llamada a **SQLAllocHandleStd** es equivalente a una llamada a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV y una llamada a **SQLSetEnvAttr** para establecer SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3.  
  
 En ciertas arquitecturas de controlador, es necesario que el controlador aparezca como un controlador ODBC *2.x* o un controlador ODBC *3.x,* dependiendo de la conexión. Es posible que el controlador en este caso no sea realmente un controlador, sino una capa que reside entre el Administrador de controladores y otro controlador. Por ejemplo, podría imitar un controlador, como ODBC Spy. En otro ejemplo, podría actuar como puerta de enlace, como EDA/SQL. Para que aparezca como un controlador ODBC *3.x,* dicho controlador debe poder exportar **SQLAllocHandle**y aparecer como un controlador ODBC *2.x,* debe poder exportar **SQLAllocConnect**, **SQLAllocEnv**y **SQLAllocStmt**. Cuando se va a asignar un entorno, una conexión o una instrucción, el Administrador de controladores comprueba si este controlador exporta **SQLAllocHandle**. Puesto que lo hace el controlador, el Administrador de controladores llama a **SQLAllocHandle** en el controlador. Si el controlador está trabajando con un controlador ODBC *2.x,* el controlador debe asignar la llamada a **SQLAllocHandle** a **SQLAllocConnect**, **SQLAllocEnv**o **SQLAllocStmt**, según corresponda. También debe hacer nada con la llamada **SQLSetEnvAttr** al comportarse como un controlador ODBC *2.x.*  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de datos de fecha y hora](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [Compatibilidad con versiones anteriores de los tipos de datos de C](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [Marcadores de longitud fija](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [Compatibilidad con SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [Devuelve SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [Llamar a SQLSetPos para insertar datos](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [Cargar por ordinal](../../../odbc/reference/appendixes/loading-by-ordinal.md)
