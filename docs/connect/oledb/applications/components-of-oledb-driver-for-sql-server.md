---
title: Los componentes del controlador OLE DB para SQL Server | Microsoft Docs
description: Componentes del controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b1b46e57b3be42fa93f8a246db528a5f85709d9e
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109837"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Componentes del controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Controlador OLE DB para SQL Server contiene los siguientes componentes:  

|Componente|Descripción|  
|---------------|-----------------|  
|msoledbsql.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene todo el controlador OLE DB para la funcionalidad de SQL Server.|  
|msoledbsqlr.rll|El archivo de recursos que lo acompaña para el controlador OLE DB para la biblioteca de SQL Server.|   
|msoledbsql.h|El controlador OLE DB para el archivo de encabezado de SQL Server que contiene todas las definiciones nuevas necesarias para poder usar el controlador de OLE DB para SQL Server. Este archivo de encabezado reemplaza el archivo de encabezado sqloledb.h.<br /><br /> Nota: Puede hacer referencia msoledbsql.h y sqloledb.h en el mismo programa, siempre sqloledb.h se defina en primer lugar.|  
|msoledbsql.lib|El archivo de biblioteca necesario para directamente llamada la [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) función que forma parte del controlador OLE DB para SQL Server.<br /><br /> Nota: Si hace referencia al archivo msoledbsql.lib en el código de programación, tiene que asegurarse de que el archivo msoledbsql.lib está en la ruta de acceso de su sistema y en la del sistema de los usuarios que usan la aplicación.|  

## <a name="see-also"></a>Ver también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
