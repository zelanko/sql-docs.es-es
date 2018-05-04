---
title: Identificadores de conexión | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb5ce0df72f4616f89fc3ab52b7b96036e96436b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="connection-handles"></a>Identificadores de conexión
A *conexión* consta de un controlador y un origen de datos. Un identificador de conexión identifica cada conexión. El identificador de conexión define qué controlador debe usar, pero no solo qué origen de datos para usarlo con ese controlador. Dentro de un segmento de código que implementa ODBC (el Administrador de controladores o un controlador), el identificador de conexión identifica una estructura que contiene información de conexión, como las siguientes:  
  
-   El estado de la conexión  
  
-   Los diagnósticos de nivel de conexión actuales  
  
-   Los identificadores de instrucciones y los descriptores de asignación actual en la conexión  
  
-   La configuración actual de cada atributo de conexión  
  
 ODBC no evita que varias conexiones simultáneas, si el controlador es compatible con ellos. Por lo tanto, en un entorno de ODBC determinado, varios identificadores de conexión pueden señalar a una variedad de controladores y orígenes de datos, en el mismo controlador y una gran variedad de orígenes de datos, o incluso varias conexiones con el mismo controlador y el origen de datos. Algunos controladores de limitan el número de conexiones activas que admiten; opción el SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo** especifica cuántas conexiones activas que admite un controlador determinado.  
  
 Identificadores de conexión se utilizan principalmente al conectarse al origen de datos (**SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**), desconectar de los datos origen (**SQLDisconnect**), obtener información sobre el origen de datos y el controlador (**SQLGetInfo**), la recuperación de diagnóstico (**SQLGetDiagField** y **SQLGetDiagRec**) y realizar transacciones (**SQLEndTran**). También se utilizan al establecer u obtener atributos de conexión (**SQLSetConnectAttr** y **SQLGetConnectAttr**) y al obtener el formato nativo de una instrucción SQL (**SQLNativeSql** ).  
  
 Se asignan a identificadores de conexión **SQLAllocHandle** y liberado con **SQLFreeHandle**.
