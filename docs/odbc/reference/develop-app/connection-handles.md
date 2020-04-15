---
title: Manijas de conexión ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d5b03e0733e35984350d2a218b885dc148ca8f8f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299025"
---
# <a name="connection-handles"></a>Identificadores de conexión
Una *conexión* consta de un controlador y un origen de datos. Un identificador de conexión identifica cada conexión. El identificador de conexión define no solo qué controlador usar, sino qué origen de datos usar con ese controlador. Dentro de un segmento de código que implementa ODBC (el Administrador de controladores o un controlador), el identificador de conexión identifica una estructura que contiene información de conexión, como la siguiente:  
  
-   El estado de la conexión  
  
-   El diagnóstico actual a nivel de conexión  
  
-   Los identificadores de instrucciones y descriptores asignados actualmente en la conexión  
  
-   La configuración actual de cada atributo de conexión  
  
 ODBC no impide varias conexiones simultáneas, si el controlador las admite. Por lo tanto, en un entorno ODBC determinado, varios identificadores de conexión pueden apuntar a una variedad de controladores y orígenes de datos, al mismo controlador y a una variedad de orígenes de datos, o incluso a varias conexiones al mismo controlador y origen de datos. Algunos controladores limitan el número de conexiones activas que admiten; la opción SQL_MAX_DRIVER_CONNECTIONS de **SQLGetInfo** especifica cuántas conexiones activas admite un controlador determinado.  
  
 Los identificadores de conexión se utilizan principalmente al conectarse al origen de datos (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**), desconectarse del origen de datos (**SQLDisconnect**), obtener información sobre el controlador y el origen de datos (**SQLGetInfo**), recuperar diagnósticos (**SQLGetDiagField** y **SQLGetDiagRec**) y realizar transacciones (**SQLEndTran**). También se utilizan al establecer y obtener atributos de conexión (**SQLSetConnectAttr** y **SQLGetConnectAttr**) y al obtener el formato nativo de una instrucción SQL (**SQLNativeSql**).  
  
 Los identificadores de conexión se asignan con **SQLAllocHandle** y se liberan con **SQLFreeHandle**.
