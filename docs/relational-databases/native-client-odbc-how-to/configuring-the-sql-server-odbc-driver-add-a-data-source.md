---
title: Agregar un origen de datos (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: d8c6111d04f9cb6409d371152afb47b528f1ebb7
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39551675"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>Configurar el controlador ODBC de SQL Server: agregar un origen de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Antes de utilizar las aplicaciones ODBC con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, debe saber cómo actualizar la versión de los procedimientos almacenados del catálogo en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y agregar, eliminar y probar los orígenes de datos.  
  
  Puede agregar un origen de datos con el Administrador de ODBC, mediante programación (utilizando [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)), o mediante la creación de un archivo.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Para agregar un origen de datos mediante el Administrador ODBC  
  
1.  Desde el **Panel de Control**, acceso **herramientas administrativas** y, después, **orígenes de datos ODBC (64 bits)** o **orígenes de datos ODBC (32-bit)**. De modo alternativo, puede invocar odbcad32.exe.  
  
2.  Haga clic en el **DSN de usuario**, **DSN de sistema**, o **DSN de archivo** pestaña y, a continuación, haga clic en **agregar**.  
  
3.  Haga clic en **SQL Server**y, a continuación, haga clic en **finalizar**.  
  
4.  Complete los pasos de la **crear un nuevo origen de datos a SQL Server** asistente.  
  
### <a name="to-add-a-data-source-programmatically"></a>Para agregar un origen de datos mediante programación  
  
1.  Llame a [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) con el segundo parámetro establecido en ODBC_ADD_DSN u ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Para agregar un origen de datos de archivo  
  
1.  Llame a [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) con un SAVEFILE = nombre_archivo parámetro en la cadena de conexión. Si la conexión se realiza correctamente, el controlador ODBC crea un origen de datos de archivo con los parámetros de conexión en la ubicación señalada por el parámetro SAVEFILE.  
  
## <a name="see-also"></a>Vea también  
[Eliminar un origen de datos &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
