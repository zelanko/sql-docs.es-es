---
title: Directivas de compatibilidad del controlador OLE DB para SQL Server | Microsoft Docs
description: Directivas de compatibilidad del controlador OLE DB para SQL Server
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 6d71a4944aaf4fe15ba76c4d831f4809f5278f83
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021748"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Directivas de compatibilidad del controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artículo describe cómo los distintos componentes de acceso a datos pueden utilizarse con el controlador de OLE DB para SQL Server.  

## <a name="server-support"></a>Compatibilidad de servidor  
 Controlador OLE DB para SQL Server admite conexiones a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)],[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], y [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versiones de sistemas operativos admitidos  
 En la tabla siguiente se enumera los sistemas operativos admitidos controlador OLE DB para SQL Server.  

|Sistemas operativos admitidos|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>Directivas de compatibilidad de ADO  
 Las aplicaciones ADO pueden usar el proveedor OLE DB SQLOLEDB que se incluye con Windows si no requieren ninguna de las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior.  

 Las aplicaciones ADO pueden usar el controlador OLE DB para SQL Server, pero si lo hacen deben especificar `DataTypeCompatibility=80` en las cadenas de conexión. Solo estarán disponibles las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] cuando `DataTypeCompatibility=80` esté presente en las cadenas de conexión.  

## <a name="ole-db-support-policies"></a>Directivas de soporte de OLE DB  
Las aplicaciones pueden usar el proveedor OLE DB (SQLOLEDB) que se incluye con el sistema operativo Windows. Sin embargo, que está en modo de mantenimiento y ya no se actualiza. Debe usar el controlador OLE DB para SQL Server (MSOLEDBSQL) en su lugar.

## <a name="see-also"></a>Ver también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
