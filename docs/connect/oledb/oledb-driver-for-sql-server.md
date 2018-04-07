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
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 5f009cf311c1eb395915e017bf202abea5ae5290
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL o controlador OLE DB para SQL Server, es un término que se usa indistintamente para hacer referencia al controlador de OLE DB para SQL Server.

## <a name="different-generations-of-ole-db-drivers"></a>Diferentes generaciones de controladores de OLE DB

Hay tres generaciones distintas de proveedores de Microsoft OLE DB para SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Proveedor Microsoft OLE DB para SQL Server (SQLOLEDB)
El [proveedor Microsoft OLE DB para SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) todavía se incluye como parte del [Windows Data Access Components](https://msdn.microsoft.com/en-us/library/ms692897.aspx). No se mantiene ya y no se recomienda utilizar este controlador para el nuevo desarrollo. 


### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)
A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) incluye una interfaz de proveedor de OLE DB (SQLNCLI) y es el proveedor OLE DB que se incluye con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a través de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Era [anunció su eliminación en 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) y no se recomienda utilizar este controlador para el nuevo desarrollo. Para obtener más información sobre el ciclo de vida SNAC y descargas disponibles, consulte [ciclo de vida SNAC explicada](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Controlador de Microsoft OLE DB para SQL Server (MSOLEDBSQL)
OLE DB [undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) y publicadas en 2018 y se puede descargar [aquí](https://go.microsoft.com/fwlink/?linkid=871294).

El nuevo proveedor de OLE DB se llama el controlador OLE DB de Microsoft para SQL Server (MSOLEDBSQL). El nuevo proveedor se actualizará con las últimas características de servidor en el futuro.

> [!NOTE]
> Para usar el controlador de OLE DB para Microsoft nueva para SQL Server en las aplicaciones existentes, debe planear convertir las cadenas de conexión de SQLOLEDB o SQLNCLI, a MSOLEDBSQL.   

Obtener información sobre el controlador OLE DB para características de SQL Server:

-   [Controlador OLE DB para la compatibilidad de SQL Server con LocalDB](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [Detección de metadatos](../oledb/features/metadata-discovery.md)  

-   [Compatibilidad de UTF-16 con el controlador OLE DB para SQL Server](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [Controlador OLE DB para la compatibilidad de SQL Server con la alta disponibilidad y la recuperación ante desastres](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [Obtener acceso a información de diagnóstico en el registro de eventos extendidos](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>Vea también  
[Instale el controlador OLE DB para SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)     
[Controlador OLE DB para las características de SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )     
