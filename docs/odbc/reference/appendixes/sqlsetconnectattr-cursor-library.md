---
title: SQLSetConnectAttr (biblioteca de cursores) | Documentos de Microsoft
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
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bf6a14b8215f981e5e0e9c0ca6e9b2e1a2269f65
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLSetConnectAttr** función en la biblioteca de cursores. Para obtener información general sobre **SQLSetConnectAttr**, consulte [función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Una aplicación llama **SQLSetConnectAttr** con el atributo SQL_ATTR_ODBC_CURSORS para especificar si la biblioteca de cursores se utiliza siempre, usa si el controlador no es compatible con los cursores desplazables o nunca se utiliza. La biblioteca de cursores se da por supuesto que un controlador es compatible con los cursores desplazables si devuelve SQL_CA1_RELATIVE para el tipo de información de SQL_STATIC_CURSOR_ATTRIBUTES1 en **SQLGetInfo**.  
  
 La aplicación debe llamar a **SQLSetConnectAttr** para especificar el uso de la biblioteca de cursores después de llamar a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC para asignar la conexión y antes de conectarse al origen de datos. Si una aplicación llama **SQLSetConnectAttr** con el atributo SQL_ATTR_ODBC_CURSORS mientras la conexión está activa, la biblioteca de cursores devuelve un error.  
  
 Para establecer un atributo de instrucción admitido por la biblioteca de cursores para todas las instrucciones asociadas a una conexión, debe llamar una aplicación **SQLSetConnectAttr** para ese atributo de instrucción después de conectarse al origen de datos y antes de que se abre el cursor. Si una aplicación llama **SQLSetConnectAttr** con una declaración de atributo y un cursor está abierto en una instrucción asociada a la conexión, el atributo de instrucción no se aplicará a esa instrucción hasta que se cierra el cursor y volver a abrir.

