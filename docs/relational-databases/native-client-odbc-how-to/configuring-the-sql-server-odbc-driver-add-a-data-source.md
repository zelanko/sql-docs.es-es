---
title: Agregar un origen de datos (ODBC) | Microsoft Docs
description: Obtenga información acerca de cómo SQL Server controlador ODBC llama a procedimientos almacenados como procedimientos almacenados remotos en SQL Server mediante el mecanismo de llamada a procedimiento almacenado remoto.
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [ODBC]
ms.assetid: b4ac6f0e-8e6a-4b1a-9a7e-60e0a69b2180
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f96a581a822b61e28831ff5eef61b77310f89344
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967647"
---
# <a name="configuring-the-sql-server-odbc-driver---add-a-data-source"></a>Configurar el controlador ODBC de SQL Server: agregar un origen de datos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Antes de utilizar las aplicaciones ODBC con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o una versión posterior, debe saber cómo actualizar la versión de los procedimientos almacenados del catálogo en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y agregar, eliminar y probar los orígenes de datos.  
  
  Puede Agregar un origen de datos mediante el administrador ODBC, mediante programación (mediante [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)) o mediante la creación de un archivo.  
  
### <a name="to-add-a-data-source-by-using-odbc-administrator"></a>Para agregar un origen de datos mediante el Administrador ODBC  
  
1.  En el **Panel de control**, acceda a **herramientas administrativas** y, a continuación, a **orígenes de datos ODBC (64 bits)** o a **orígenes de datos ODBC (32 bits)**. De modo alternativo, puede invocar odbcad32.exe.  
  
2.  Haga clic en la pestaña **DSN de usuario**, **DSN de sistema**o **DSN de archivo** y, a continuación, haga clic en **Agregar**.  
  
3.  Haga clic en **SQL Server**y, a continuación, en **Finalizar**.  
  
4.  Complete los pasos del asistente **para crear un nuevo origen de datos para SQL Server** .  
  
### <a name="to-add-a-data-source-programmatically"></a>Para agregar un origen de datos mediante programación  
  
1.  Llame a [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md) con el segundo parámetro establecido en ODBC_ADD_DSN o en ODBC_ADD_SYS_DSN.  
  
### <a name="to-add-a-file-data-source"></a>Para agregar un origen de datos de archivo  
  
1.  Llame a [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) con un parámetro SAVEFILE = file_name en la cadena de conexión. Si la conexión se realiza correctamente, el controlador ODBC crea un origen de datos de archivo con los parámetros de conexión en la ubicación señalada por el parámetro SAVEFILE.  
  
## <a name="see-also"></a>Consulte también  
[Eliminar un origen de datos &#40;ODBC&#41;](../../relational-databases/native-client-odbc-how-to/configuring-the-sql-server-odbc-driver-delete-a-data-source.md)    
  
  
