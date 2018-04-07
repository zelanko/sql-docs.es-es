---
title: Directivas de soporte para el controlador OLE DB para SQL Server | Documentos de Microsoft
description: Directivas de soporte técnico para el controlador OLE DB para SQL Server
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 374660fdba66e5c445ae441d988a3701de548427
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Directivas de soporte técnico para el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Este artículo describe cómo los distintos componentes de acceso a datos se pueden utilizar con el controlador OLE DB para SQL Server.  

## <a name="server-support"></a>Compatibilidad de servidor  
 Controlador de OLE DB para SQL Server admite las conexiones a [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)],[!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], y [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versiones de sistemas operativos admitidos  
 En la tabla siguiente se enumera los sistemas operativos admitidos controlador OLE DB para SQL Server.  

|Sistemas operativos compatibles|  
|--------------------------------------|---------------------------------|   
|Microsoft Windows 8.1<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012<br /><br />Microsoft Windows Server 2012 R2<br /><br />Microsoft Windows Server 2016|  

## <a name="ado-support-policies"></a>Directivas de compatibilidad de ADO  
 Las aplicaciones ADO pueden usar el proveedor OLE DB SQLOLEDB que se incluye con Windows si no requieren ninguna de las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior.  

 Aplicaciones ADO pueden usar el controlador OLE DB para SQL Server, pero si lo hacen, debe especificar `DataTypeCompatibility=80` en las cadenas de conexión. Solo estarán disponibles las características de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] cuando `DataTypeCompatibility=80` esté presente en las cadenas de conexión.  

## <a name="ole-db-support-policies"></a>Directivas de soporte de OLE DB  
Aplicaciones pueden usar el proveedor de OLE DB (SQLOLEDB) incluido con el sistema operativo Windows. Sin embargo, que está en modo de mantenimiento y ya no se actualiza. Debe usar el controlador OLE DB para SQL Server (MSOLEDBSQL) en su lugar.

## <a name="see-also"></a>Vea también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
