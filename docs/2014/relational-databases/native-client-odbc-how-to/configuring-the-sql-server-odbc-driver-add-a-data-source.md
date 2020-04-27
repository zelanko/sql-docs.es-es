---
title: Agregar un origen de datos (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c050efd2f309ccec76b80fd24b519e7d2389e4ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63126079"
---
# <a name="add-a-data-source-odbc"></a>Agregar un origen de datos (ODBC)
  Puede Agregar un origen de datos mediante el administrador ODBC, mediante programación (mediante [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)) o mediante la creación de un archivo.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Para agregar un origen de datos mediante el Administrador ODBC  
  
1.  En el **Panel de control**, acceda a **herramientas administrativas** y, a continuación, a **orígenes de datos (ODBC)**. De modo alternativo, puede invocar odbcad32.exe.  
  
2.  Haga clic en la pestaña **DSN de usuario**, **DSN de sistema**o **DSN de archivo** y, a continuación, haga clic en **Agregar**.  
  
3.  Haga clic en **SQL Server**y, a continuación, en **Finalizar**.  
  
4.  Complete los pasos del Asistente para crear un nuevo origen de datos para SQL Server.  
  
### <a name="to-add-a-data-source-programmatically"></a>Para agregar un origen de datos mediante programación  
  
1.  Llame a [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) con el segundo parámetro establecido en ODBC_ADD_DSN o en ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Para agregar un origen de datos de archivo  
  
1.  Llame a [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) con un parámetro SAVEFILE = file_name en la cadena de conexión. Si la conexión se realiza correctamente, el controlador ODBC crea un origen de datos de archivo con los parámetros de conexión en la ubicación señalada por el parámetro SAVEFILE.  
  
## <a name="see-also"></a>Consulte también  
 [Temas de procedimientos de configuración del controlador ODBC de SQL Server](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  
