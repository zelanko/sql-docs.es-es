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
ms.openlocfilehash: ab8b94835fb9a6103436026a669c86f2401d57b0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036433"
---
# <a name="connection-handles"></a>Identificadores de conexión
Una *conexión* consta de un controlador y un origen de datos. Un identificador de conexión identifica cada conexión. El identificador de conexión define no solo el controlador que se va a usar pero el origen de datos que se va a usar con ese controlador. Dentro de un segmento de código que implementa ODBC (el administrador de controladores o un controlador), el identificador de conexión identifica una estructura que contiene información de conexión, como la siguiente:  
  
-   El estado de la conexión.  
  
-   Diagnósticos en el nivel de conexión actual  
  
-   Los identificadores de instrucciones y descriptores asignados actualmente en la conexión.  
  
-   La configuración actual de cada atributo de conexión  
  
 ODBC no impide varias conexiones simultáneas, si el controlador las admite. Por lo tanto, en un entorno ODBC determinado, varios identificadores de conexión pueden apuntar a una variedad de controladores y orígenes de datos, al mismo controlador y a una variedad de orígenes de datos, o incluso a varias conexiones al mismo controlador y origen de datos. Algunos controladores limitan el número de conexiones activas que admiten; la opción SQL_MAX_DRIVER_CONNECTIONS de **SQLGetInfo** especifica el número de conexiones activas que admite un controlador determinado.  
  
 Los identificadores de conexión se utilizan principalmente cuando se conecta al origen de datos (**SQLConnect**, **SQLDriverConnect**o **SQLBrowseConnect**), se desconecta del origen de datos (**SQLDisconnect**), se obtiene información sobre el controlador y el origen de datos (**SQLGetInfo**), se recuperan los diagnósticos (**SQLGetDiagField** y **SQLGetDiagRec**) y se realizan transacciones (**SQLEndTran**). También se usan al establecer y obtener atributos de conexión (**SQLSetConnectAttr** y **SQLGetConnectAttr**) y al obtener el formato nativo de una instrucción SQL (**SQLNativeSql**).  
  
 Los identificadores de conexión se asignan con **SQLAllocHandle** y se liberan con **SQLFreeHandle**.
