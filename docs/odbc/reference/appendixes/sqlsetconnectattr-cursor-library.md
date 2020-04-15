---
title: SQLSetConnectAttr (Biblioteca de cursores) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectAttr function [ODBC], Cursor Library
ms.assetid: 6f70bbd0-a057-49ef-8b05-4c80b58fc6e6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a87c85d727fb9eb2fc27613b9eecd3fe0ec51b58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300545"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLSetConnectAttr** en la biblioteca de cursores. Para obtener información general sobre **SQLSetConnectAttr**, vea [Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Una aplicación llama a **SQLSetConnectAttr** con el atributo SQL_ATTR_ODBC_CURSORS para especificar si siempre se utiliza la biblioteca de cursores, se usa si el controlador no admite cursores desplazables o nunca se usa. La biblioteca de cursores supone que un controlador admite cursores desplazables si devuelve SQL_CA1_RELATIVE para el tipo de información SQL_STATIC_CURSOR_ATTRIBUTES1 en **SQLGetInfo**.  
  
 La aplicación debe llamar a **SQLSetConnectAttr** para especificar el uso de la biblioteca de cursores después de llamar a **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC para asignar la conexión y antes de que se conecte al origen de datos. Si una aplicación llama a **SQLSetConnectAttr** con el atributo SQL_ATTR_ODBC_CURSORS mientras la conexión sigue activa, la biblioteca de cursores devuelve un error.  
  
 Para establecer un atributo de instrucción admitido por la biblioteca de cursores para todas las instrucciones asociadas a una conexión, una aplicación debe llamar a **SQLSetConnectAttr** para ese atributo de instrucción después de conectarse al origen de datos y antes de abrir el cursor. Si una aplicación llama a **SQLSetConnectAttr** con un atributo de instrucción y un cursor está abierto en una instrucción asociada a la conexión, el atributo de instrucción no se aplicará a esa instrucción hasta que el cursor se cierre y se vuelva a abrir.
