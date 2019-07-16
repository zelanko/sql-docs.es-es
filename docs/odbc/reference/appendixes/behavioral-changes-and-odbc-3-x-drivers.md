---
title: Cambios de comportamiento y controladores ODBC 3.x | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27b48951c6fb3be8bfe070863409d77ab760d5fc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915615"
---
# <a name="behavioral-changes-and-odbc-3x-drivers"></a>Cambios de comportamiento y controladores ODBC 3.x
El atributo de entorno SQL_ATTR_ODBC_VERSION indica al controlador si se debe presentar ODBC *2.x* comportamiento u ODBC *3.x* comportamiento. ¿Cómo se establece el atributo de entorno SQL_ATTR_ODBC_VERSION depende de la aplicación. ODBC *3.x* deben llamar las aplicaciones **SQLSetEnvAttr** para establecer este atributo, una vez que llame a **SQLAllocHandle** para asignar un identificador de entorno y antes de llamar a  **SQLAllocHandle** para asignar un identificador de conexión. Si no pueden hacer esto, el Administrador de controladores devuelve SQLSTATE HY010 (función de error de secuencia) en la última llamada a **SQLAllocHandle**.  
  
> [!NOTE]  
>  Para obtener más información sobre los cambios de comportamiento y cómo debe actuar ante una aplicación, consulte [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 ODBC *2.x* aplicaciones y ODBC *2.x* aplicaciones vuelven a compilar con ODBC *3.x* no llame los archivos de encabezado **SQLSetEnvAttr**. Sin embargo, llama **SQLAllocEnv** en lugar de **SQLAllocHandle** para asignar un identificador de entorno. Por lo tanto, cuando la aplicación llama **SQLAllocEnv** en el Administrador de controladores, el Administrador de controladores llama **SQLAllocHandle** y **SQLSetEnvAttr** en el controlador. Por lo tanto, ODBC *3.x* controladores siempre pueden contar con este atributo que se va a establecer.  
  
 Si una aplicación compatible con los estándares compilado con la marca de compilación ODBC_STD llamadas **SQLAllocEnv** (que puede producirse porque **SQLAllocEnv** no está en desuso en ISO), la llamada se asigna a  **SQLAllocHandleStd** en tiempo de compilación. En tiempo de ejecución, la aplicación llama a **SQLAllocHandleStd**. El Administrador de controladores se establece el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3. Una llamada a **SQLAllocHandleStd** es equivalente a una llamada a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_ENV y una llamada a **SQLSetEnvAttr** establecer SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC3.  
  
 En ciertas arquitecturas de controlador, es necesario para que el controlador aparecen como un ODBC *2.x* controlador o un ODBC *3.x* controlador, dependiendo de la conexión. El controlador en este caso podría no constituir un controlador, pero una capa que se encuentra entre el Administrador de controladores y otro controlador. Por ejemplo, podría ser como un controlador, como ODBC Spy. En otro ejemplo, puede actuar como una puerta de enlace, como EDA/SQL. Aparezca como un ODBC *3.x* controlador, este tipo de controlador debe poder exportar **SQLAllocHandle**y que aparezca como un ODBC *2.x* controlador, debe poder exportar  **SQLAllocConnect**, **SQLAllocEnv**, y **SQLAllocStmt**. Cuando un entorno, conexión o instrucción se va a asignar a, el Administrador de controladores comprueba para ver si exporta este controlador **SQLAllocHandle**. Puesto que el controlador realiza, las llamadas del Administrador de controladores **SQLAllocHandle** en el controlador. Si el controlador está trabajando con un ODBC *2.x* controlador, el controlador debe asignar la llamada a **SQLAllocHandle** a **SQLAllocConnect**, **SQLAllocEnv**, o **SQLAllocStmt**, según corresponda. También debe hacer nada con la **SQLSetEnvAttr** llamar cuando se comporta como un ODBC *2.x* controlador.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Tipos de datos de fecha y hora](../../../odbc/reference/appendixes/datetime-data-types.md)  
  
-   [Compatibilidad con versiones anteriores de los tipos de datos de C](../../../odbc/reference/appendixes/backward-compatibility-of-c-data-types.md)  
  
-   [Marcadores de longitud fija](../../../odbc/reference/appendixes/fixed-length-bookmarks.md)  
  
-   [Compatibilidad con SQLGetInfo](../../../odbc/reference/appendixes/sqlgetinfo-support.md)  
  
-   [Devuelve SQL_NO_DATA](../../../odbc/reference/appendixes/returning-sql-no-data.md)  
  
-   [Llamar a SQLSetPos para insertar datos](../../../odbc/reference/appendixes/calling-sqlsetpos-to-insert-data.md)  
  
-   [Cargar por ordinal](../../../odbc/reference/appendixes/loading-by-ordinal.md)
