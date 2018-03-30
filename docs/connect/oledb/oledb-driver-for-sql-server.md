---
title: Controlador OLE DB para SQL Server | Documentos de Microsoft
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
description: ''
ms.custom: ''
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 89e66fe2c61ae17a43e2a58071ba04374f33ea04
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL o controlador OLE DB para SQL Server, es un término que se ha utilizado indistintamente para hacer referencia al controlador de OLE DB para SQL Server.

## <a name="different-incarnations-of-ole-db-drivers"></a>Versiones diferentes de los controladores OLE DB

Hay tres versiones distintas de los proveedores de OLE DB de Microsoft para SQL Server.


### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Proveedor Microsoft OLE DB para SQL Server (SQLOLEDB)

El [proveedor Microsoft OLE DB para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) todavía se incluye como parte del [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx). No se recomienda utilizar este controlador para el nuevo desarrollo.


### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)

A partir de SQL Server 2005, la [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) incluye una interfaz de proveedor de OLE DB (SQLNCLI) y es el proveedor OLE DB que se incluye con SQL Server 2005 mediante SQL Server 2017.

Era [anunció su eliminación en 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) y no se recomienda utilizar este controlador para el nuevo desarrollo.


### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Controlador de Microsoft OLE DB para SQL Server (MSOLEDBSQL)

OLE DB [anuncia como con undeprecated en 2017](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/). Se presentó una nueva versión planeada para 2018.

El nuevo proveedor de OLE DB se llama el controlador OLE DB de Microsoft para SQL Server (MSOLEDBSQL). El nuevo proveedor se actualizará con las últimas características de servidor en el futuro.

Obtener información sobre el controlador OLE DB para características de SQL Server:

-   [Controlador OLE DB para SQL Server Support for LocalDB](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [Detección de metadatos](../oledb/features/metadata-discovery.md)  

-   [Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [Controlador OLE DB para SQL Server Support for High Availability, Disaster Recovery](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [Obtener acceso a información de diagnóstico en el registro de eventos extendidos](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>Vea también  
[Instale el controlador OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
 [Controlador OLE DB para características de SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )  
