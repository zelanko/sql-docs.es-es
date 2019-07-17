---
title: SQLSetConnectAttr (biblioteca de cursores) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 73d1369a2bce0327ac3367d33f0894bdcfab8205
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125581"
---
# <a name="sqlsetconnectattr-cursor-library"></a>SQLSetConnectAttr (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLSetConnectAttr** función en la biblioteca de cursores. Para obtener información general sobre **SQLSetConnectAttr**, consulte [función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md).  
  
 Una aplicación llama a **SQLSetConnectAttr** con el atributo SQL_ATTR_ODBC_CURSORS para especificar si la biblioteca de cursores se utiliza siempre, usa si el controlador no es compatible con los cursores desplazables o nunca se utiliza. La biblioteca de cursores se da por supuesto que un controlador es compatible con los cursores desplazables si devuelve SQL_CA1_RELATIVE para el tipo de información SQL_STATIC_CURSOR_ATTRIBUTES1 **SQLGetInfo**.  
  
 La aplicación debe llamar a **SQLSetConnectAttr** para especificar el uso de la biblioteca de cursores después de llamar al **SQLAllocHandle** con un *HandleType* de SQL_HANDLE_DBC para asignar la conexión y antes de conectarse al origen de datos. Si una aplicación llama a **SQLSetConnectAttr** con el atributo SQL_ATTR_ODBC_CURSORS mientras la conexión está activa, la biblioteca de cursores devuelve un error.  
  
 Para establecer un atributo de instrucción compatible con la biblioteca de cursores para todas las instrucciones asociadas con una conexión, debe llamar una aplicación **SQLSetConnectAttr** para ese atributo de instrucción después de conectarse al origen de datos y antes de que se abre el cursor. Si una aplicación llama a **SQLSetConnectAttr** con una instrucción de atributo y un cursor está abierto en una instrucción asociada con la conexión, el atributo de instrucción no se aplicará a esa instrucción hasta que se cierra el cursor y volver a abrir.
