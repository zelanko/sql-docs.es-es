---
title: Identificadores de conexión | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77fdb63f346ada40346544a53c3ff69db0a8a9a4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828946"
---
# <a name="connection-handles"></a>Identificadores de conexión
Un *conexión* consta de un controlador y un origen de datos. Un identificador de conexión identifica cada conexión. El identificador de conexión define qué controlador usar, pero no sólo qué origen de datos para usar con ese controlador. Dentro de un segmento de código que implementa ODBC (el Administrador de controladores o un controlador), el identificador de conexión identifica una estructura que contiene información de conexión, como la siguiente:  
  
-   El estado de la conexión  
  
-   Los diagnósticos de nivel de conexión actuales  
  
-   Los identificadores de instrucciones y descriptores asignados actualmente en la conexión  
  
-   La configuración actual de cada atributo de conexión  
  
 ODBC no impide que varias conexiones simultáneas, si el controlador es compatible con ellos. Por lo tanto, en un entorno de ODBC determinado, varios identificadores de conexión podrían apuntar a una variedad de controladores y orígenes de datos, en el mismo controlador y una variedad de orígenes de datos, o incluso a múltiples conexiones con el mismo controlador y el origen de datos. Algunos controladores de limitan el número de conexiones activas que admiten; opción el SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo** especifica cuántas conexiones activas que admite un controlador determinado.  
  
 Identificadores de conexión se utilizan principalmente al conectarse al origen de datos (**SQLConnect**, **SQLDriverConnect**, o **SQLBrowseConnect**), desconectar de los datos origen (**SQLDisconnect**), obtener información sobre el origen de datos y el controlador (**SQLGetInfo**), recuperar diagnósticos (**SQLGetDiagField** y **SQLGetDiagRec**) y realizar transacciones (**SQLEndTran**). También se usan al establecer y obtener los atributos de conexión (**SQLSetConnectAttr** y **SQLGetConnectAttr**) y al obtener el formato nativo de una instrucción SQL (**SQLNativeSql** ).  
  
 Identificadores de conexión se asignan con **SQLAllocHandle** y liberado con **SQLFreeHandle**.
