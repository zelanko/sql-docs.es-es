---
title: Directivas de compatibilidad del controlador OLE DB para SQL Server | Microsoft Docs
description: Directivas de compatibilidad del controlador OLE DB para SQL Server
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b02789c787266a3370e3c5c9bfae50ea337d19db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "72381860"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Directivas de compatibilidad del controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este tema se describe la forma de usar diversos componentes de acceso a datos con OLE DB Driver for SQL Server.  

## <a name="server-support"></a>Compatibilidad de servidor  
 OLE DB Driver for SQL Server admite conexiones a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] través de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versiones de sistemas operativos admitidos  
 En la tabla siguiente se enumeran los sistemas operativos admitidos por OLE DB Driver for SQL Server.  

| Sistemas operativos admitidos |  |
|--------------------------------------|---------------------------------|   
| Microsoft Windows 8.1 + [actualización de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [actualización de abril de 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016<br /><br />Microsoft Windows Server 2019 |  |


## <a name="ado-support-policies"></a>Directivas de compatibilidad de ADO  
 Las aplicaciones ADO pueden usar el proveedor OLE DB SQLOLEDB que se incluye con Windows si no requieren ninguna de las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior.  

 Las aplicaciones ADO también pueden usar OLE DB Driver for SQL Server pero, si lo hacen, deben especificar `DataTypeCompatibility=80` en las cadenas de conexión. Solo estarán disponibles las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] cuando `DataTypeCompatibility=80` esté presente en las cadenas de conexión.  

## <a name="ole-db-support-policies"></a>Directivas de soporte de OLE DB  
Las aplicaciones pueden usar el proveedor OLE DB (SQLOLEDB) que se incluye con el sistema operativo Windows. Aunque esto está en modo de mantenimiento y ya no se actualiza. En su lugar, use OLE DB Driver for SQL Server (MSOLEDBSQL).

## <a name="see-also"></a>Consulte también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
