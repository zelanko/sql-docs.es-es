---
title: Agregar un origen de datos (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 822ac0f5d2e228a982368849ed1c409ef63765ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198897"
---
# <a name="add-a-data-source-odbc"></a>Agregar un origen de datos (ODBC)
  Puede agregar un origen de datos mediante el Administrador de ODBC, mediante programación (utilizando [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md)), o mediante la creación de un archivo.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Para agregar un origen de datos mediante el Administrador ODBC  
  
1.  Desde el **el Panel de Control**, acceso **herramientas administrativas** y, a continuación, **orígenes de datos (ODBC)**. De modo alternativo, puede invocar odbcad32.exe.  
  
2.  Haga clic en el **DSN de usuario**, **DSN de sistema**, o **DSN de archivo** ficha y, a continuación, haga clic en **agregar**.  
  
3.  Haga clic en **SQL Server**y, a continuación, haga clic en **finalizar**.  
  
4.  Complete los pasos del Asistente para crear un nuevo origen de datos para SQL Server.  
  
### <a name="to-add-a-data-source-programmatically"></a>Para agregar un origen de datos mediante programación  
  
1.  Llame a [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md) con el segundo parámetro establecido en ODBC_ADD_DSN u ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Para agregar un origen de datos de archivo  
  
1.  Llame a [SQLDriverConnect](../native-client-odbc-api/sqldriverconnect.md) con un SAVEFILE = nombre_archivo parámetro en la cadena de conexión. Si la conexión se realiza correctamente, el controlador ODBC crea un origen de datos de archivo con los parámetros de conexión en la ubicación señalada por el parámetro SAVEFILE.  
  
## <a name="see-also"></a>Vea también  
 [Configuración de los temas "Cómo..." del controlador ODBC de SQL Server](../../database-engine/dev-guide/configuring-the-sql-server-odbc-driver-how-to-topics.md)  
  
  