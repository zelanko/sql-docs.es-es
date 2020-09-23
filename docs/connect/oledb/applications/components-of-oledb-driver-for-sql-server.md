---
title: Componentes del controlador OLE DB para SQL Server | Microsoft Docs
description: Obtenga información sobre los componentes de OLE DB Driver for SQL Server, incluida la biblioteca que contiene la funcionalidad del controlador, otras bibliotecas y un archivo de encabezado.
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa548f34701565a5fcfd836232544bc0ee1345f4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862064"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Componentes del controlador OLE DB para SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server contiene los siguientes componentes:  

|Componente|Descripción|  
|---------------|-----------------|  
|msoledbsql.dll|El archivo de biblioteca de vínculos dinámicos (DLL) que contiene toda la funcionalidad de OLE DB Driver for SQL Server.|  
|msoledbsqlr.rll|El archivo de recursos asociado de la biblioteca de OLE DB Driver for SQL Server.|   
|msoledbsql.h|El archivo de encabezado de OLE DB Driver for SQL Server que contiene todas las definiciones nuevas necesarias para poder usar OLE DB Driver for SQL Server. Este archivo de encabezado reemplaza el archivo de encabezado sqloledb.h.<br /><br /> Nota: Puede hacer referencia a msoledbsql.h y sqloledb.h en el mismo programa, siempre que se defina primero sqloledb.h.|  
|msoledbsql.lib|El archivo de biblioteca necesario para llamar directamente a la función [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) que forma parte de OLE DB Driver for SQL Server.<br /><br /> Nota: Si hace referencia al archivo msoledbsql.lib en el código de programación, tiene que asegurarse de que el archivo msoledbsql.lib está en la ruta de acceso de su sistema y en la del sistema de los usuarios que usan la aplicación.|  

## <a name="see-also"></a>Consulte también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
