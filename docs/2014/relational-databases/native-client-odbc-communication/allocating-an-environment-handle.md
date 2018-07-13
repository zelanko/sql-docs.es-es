---
title: Asignar un identificador de entorno | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dea32df21f36220959a5c3ed49a7a927b59797ce
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425944"
---
# <a name="allocating-an-environment-handle"></a>Asignar un identificador de entorno
  Para que una aplicación pueda llamar a cualquier función ODBC, debe inicializar el entorno ODBC y asignar un identificador de entorno. Se trata del identificador de contexto global y marcador de posición del resto de los identificadores de ODBC. Para ello, una llamada a **SQLAllocHandle** con el *HandleType* parámetro establecido en SQL_HANDLE_ENV y *InputHandle* establecido en SQL_NULL_HANDLE.  
  
 Después de asignar el identificador de entorno, la aplicación debe establecer atributos de entorno para indicar qué versión de las llamadas a funciones de ODBC va a utilizar. Para usar el ODBC 3. *x* llamar funciones, [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md) con el *atributo* parámetro establecido en SQL_ATTR_ODBC_VERSION y *ValuePtr* establecido en SQL_OV_ ODBC3.  
  
## <a name="see-also"></a>Vea también  
 [Comunicar con SQL Server &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
