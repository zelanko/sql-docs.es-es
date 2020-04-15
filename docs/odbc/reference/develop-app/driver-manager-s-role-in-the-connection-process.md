---
title: Driver Manager&#39;s Rol en el Proceso de conexión ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0227a4063573cb05ecaa9434605ba35f2811bd06
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305806"
---
# <a name="driver-manager39s-role-in-the-connection-process"></a>Driver Manager&#39;s Rol en el proceso de conexión
Recuerde que las aplicaciones no llaman directamente a las funciones del controlador. En su lugar, llaman a las funciones del Administrador de controladores con el mismo nombre y el Administrador de controladores llama a las funciones del controlador. Por lo general, esto sucede casi inmediatamente. Por ejemplo, la aplicación llama a **SQLExecute** en el Administrador de controladores y después de algunas comprobaciones de errores, el Administrador de controladores llama a **SQLExecute** en el controlador.  
  
 El proceso de conexión es diferente. Cuando la aplicación llama a **SQLAllocHandle** con las opciones SQL_HANDLE_ENV y SQL_HANDLE_DBC, la función asigna identificadores solo en el Administrador de controladores. El Administrador de controladores no llama a esta función en el controlador porque no sabe qué controlador llamar. De forma similar, si la aplicación pasa el identificador de una conexión no conectada a **SQLSetConnectAttr** o **SQLGetConnectAttr**, solo el Administrador de controladores ejecuta la función. Almacena u obtiene el valor de atributo de su identificador de conexión y devuelve SQLSTATE 08003 (Conexión no abierta) al obtener un valor para un atributo que no se ha establecido y para el que ODBC no define un valor predeterminado.  
  
 Cuando la aplicación llama a **SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**, el Administrador de controladores determina primero qué controlador usar. A continuación, comprueba si un controlador está cargado actualmente en la conexión:  
  
-   Si no se carga ningún controlador en la conexión, el Administrador de controladores comprueba si el controlador especificado se carga en otra conexión en el mismo entorno. Si no es así, el Administrador de controladores carga el controlador en la conexión y llama a **SQLAllocHandle** en el controlador con la opción SQL_HANDLE_ENV.  
  
     A continuación, el Administrador de controladores llama a **SQLAllocHandle** en el controlador con la opción SQL_HANDLE_DBC, independientemente de si se acaba de cargar o no. Si la aplicación establece atributos de conexión, el Administrador de controladores llama a **SQLSetConnectAttr** en el controlador; si se produce un error, la función de conexión del Administrador de controladores devuelve SQLSTATE IM006 (error en **SQLSetConnectAttr** del controlador). Por último, el Administrador de controladores llama a la función de conexión en el controlador.  
  
-   Si el controlador especificado se carga en la conexión, el Administrador de controladores llama solo a la función de conexión en el controlador. En este caso, el controlador debe asegurarse de que todos los atributos de conexión de la conexión mantienen su configuración actual.  
  
-   Si se carga un controlador diferente en la conexión, el Administrador de controladores llama a **SQLFreeHandle** en el controlador para liberar la conexión. Si no hay otras conexiones que usen el controlador, el Administrador de controladores llama a **SQLFreeHandle** en el controlador para liberar el entorno y descarga el controlador. A continuación, el Administrador de controladores realiza las mismas operaciones que cuando no se carga un controlador en la conexión.  
  
 El Administrador de controladores bloqueará el identificador de entorno (*henv*) antes de llamar a **SQLAllocHandle** y **SQLFreeHandle** de un controlador cuando *HandleType* se establece en **SQL_HANDLE_DBC**.  
  
 Cuando la aplicación llama a **SQLDisconnect**, el Administrador de controladores llama a **SQLDisconnect** en el controlador. Sin embargo, deja el controlador cargado en caso de que la aplicación se vuelva a conectar al controlador. Cuando la aplicación llama **a SQLFreeHandle** con la opción SQL_HANDLE_DBC, el Administrador de controladores llama **sqlFreeHandle** en el controlador. Si el controlador no se utiliza en otras conexiones, el Administrador de controladores, a continuación, llama a **SQLFreeHandle** en el controlador con la opción SQL_HANDLE_ENV y descarga el controlador.
