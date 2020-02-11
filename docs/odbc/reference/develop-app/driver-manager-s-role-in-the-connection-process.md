---
title: Rol&#39;s del administrador de controladores en el proceso de conexión | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver manager [ODBC], role in connection process
- connecting to data source [ODBC], driver manager
- connecting to driver [ODBC], driver manager
- ODBC driver manager [ODBC]
ms.assetid: 77c05630-5a8b-467d-b80e-c705dc06d601
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fdc7f82059579f23c9a1a1203aee5e45c87693e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046943"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>Rol&#39;s del administrador de controladores en el proceso de conexión
Recuerde que las aplicaciones no llaman directamente a las funciones de controlador. En su lugar, llaman a las funciones del administrador de controladores con el mismo nombre y el administrador de controladores llama a las funciones del controlador. Normalmente, esto sucede casi inmediatamente. Por ejemplo, la aplicación llama a **SQLExecute** en el administrador de controladores y después de algunas comprobaciones de error, el administrador de controladores llama a **SQLExecute** en el controlador.  
  
 El proceso de conexión es diferente. Cuando la aplicación llama a **SQLAllocHandle** con las opciones SQL_HANDLE_ENV y SQL_HANDLE_DBC, la función asigna solo identificadores en el administrador de controladores. El administrador de controladores no llama a esta función en el controlador porque no sabe a qué controlador debe llamar. Del mismo modo, si la aplicación pasa el identificador de una conexión desconectada a **SQLSetConnectAttr** o **SQLGetConnectAttr**, solo el administrador de controladores ejecuta la función. Almacena u obtiene el valor de atributo de su identificador de conexión y devuelve SQLSTATE 08003 (conexión no abierta) al obtener un valor para un atributo que no se ha establecido y para el que ODBC no define un valor predeterminado.  
  
 Cuando la aplicación llama a **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**, el administrador de controladores determina primero el controlador que se va a usar. A continuación, comprueba para determinar si un controlador está cargado actualmente en la conexión:  
  
-   Si no se carga ningún controlador en la conexión, el administrador de controladores comprueba si el controlador especificado está cargado en otra conexión del mismo entorno. De lo contrario, el administrador de controladores carga el controlador en la conexión y llama a **SQLAllocHandle** en el controlador con la opción SQL_HANDLE_ENV.  
  
     A continuación, el administrador de controladores llama a **SQLAllocHandle** en el controlador con la opción SQL_HANDLE_DBC, independientemente de que se haya cargado o no. Si la aplicación establece cualquier atributo de conexión, el administrador de controladores llama a **SQLSetConnectAttr** en el controlador; Si se produce un error, la función de conexión del administrador de controladores devuelve SQLSTATE IM006 (error de **SQLSetConnectAttr** del controlador). Por último, el administrador de controladores llama a la función de conexión en el controlador.  
  
-   Si el controlador especificado está cargado en la conexión, el administrador de controladores solo llama a la función de conexión del controlador. En este caso, el controlador debe asegurarse de que todos los atributos de conexión de la conexión mantienen su configuración actual.  
  
-   Si se carga un controlador diferente en la conexión, el administrador de controladores llama a **SQLFreeHandle** en el controlador para liberar la conexión. Si no hay otras conexiones que usen el controlador, el administrador de controladores llama a **SQLFreeHandle** en el controlador para liberar el entorno y descargar el controlador. A continuación, el administrador de controladores realiza las mismas operaciones que cuando no se carga un controlador en la conexión.  
  
 El administrador de controladores bloqueará el identificador de entorno (*HENV*) antes de llamar al método **SQLAllocHandle** y **SQLFreeHandle** de un controlador cuando *HandleType* está establecido en **SQL_HANDLE_DBC**.  
  
 Cuando la aplicación llama a **SQLDisconnect**, el administrador de controladores llama a **SQLDisconnect** en el controlador. Sin embargo, deja el controlador cargado en caso de que la aplicación vuelva a conectarse al controlador. Cuando la aplicación llama a **SQLFreeHandle** con la opción SQL_HANDLE_DBC, el administrador de controladores llama a **SQLFreeHandle** en el controlador. Si el controlador no lo usa ninguna otra conexión, el administrador de controladores llama a **SQLFreeHandle** en el controlador con la opción SQL_HANDLE_ENV y descarga el controlador.
