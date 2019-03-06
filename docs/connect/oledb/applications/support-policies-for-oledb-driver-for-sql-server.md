---
title: Directivas de compatibilidad del controlador OLE DB para SQL Server | Microsoft Docs
description: Directivas de compatibilidad del controlador OLE DB para SQL Server
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 790f19d136470458620e0c00de00885e079256bf
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744605"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Directivas de compatibilidad del controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Este artículo describe cómo los distintos componentes de acceso a datos pueden utilizarse con el controlador de OLE DB para SQL Server.  

## <a name="server-support"></a>Compatibilidad de servidor  
 Controlador OLE DB para SQL Server admite conexiones a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], y [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versiones de sistemas operativos admitidos  
 En la tabla siguiente se enumera los sistemas operativos admitidos controlador OLE DB para SQL Server.  

|Sistemas operativos admitidos|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1 + [actualización de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [actualización de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>Directivas de compatibilidad de ADO  
 Las aplicaciones ADO pueden usar el proveedor OLE DB SQLOLEDB que se incluye con Windows si no requieren ninguna de las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior.  

 Las aplicaciones ADO pueden usar el controlador OLE DB para SQL Server, pero si lo hacen deben especificar `DataTypeCompatibility=80` en las cadenas de conexión. Solo estarán disponibles las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] cuando `DataTypeCompatibility=80` esté presente en las cadenas de conexión.  

## <a name="ole-db-support-policies"></a>Directivas de soporte de OLE DB  
Las aplicaciones pueden usar el proveedor OLE DB (SQLOLEDB) que se incluye con el sistema operativo Windows. Sin embargo, que está en modo de mantenimiento y ya no se actualiza. Use el controlador OLE DB para SQL Server (MSOLEDBSQL) en su lugar.

## <a name="see-also"></a>Vea también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
