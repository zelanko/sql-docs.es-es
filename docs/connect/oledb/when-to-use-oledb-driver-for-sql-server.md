---
title: Casos de uso de OLE DB Driver
description: Obtenga información sobre cuándo usar OLE DB Driver for SQL Server y los conceptos de acceso a datos de alto nivel que lo diferencian de otros controladores.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 4f3ec9e3eee38b5ba6f2c0140a1f6eb316941a02
ms.sourcegitcommit: 66407a7248118bb3e167fae76bacaa868b134734
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/21/2020
ms.locfileid: "81727958"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>Casos de uso del controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server es una tecnología que se puede usar para acceder a los datos de una base de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Para obtener una explicación de las distintas tecnologías de acceso a datos, vea [Data Access Technologies Road Map](https://go.microsoft.com/fwlink/?LinkID=179186) (Guía básica de las tecnologías de acceso a datos).  
  
 A la hora de decidir si debe usar el controlador OLE DB para SQL Server como la tecnología de acceso a datos de la aplicación, debe tener en cuenta varios factores.  
  
 En el caso aplicaciones nuevas, si está utilizando un lenguaje de programación administrado, como Microsoft Visual C# o Visual Basic, y necesita obtener acceso a las nuevas características introducidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debería utilizar el proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que forma parte de .NET Framework.  
  
 Si está desarrollando una aplicación basada en COM y necesita obtener acceso a las nuevas características introducidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debería usar el controlador OLE DB para SQL Server. Si no necesita obtener acceso a las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede seguir utilizando Windows Data Access Components (WDAC).  
  
 En el caso de las aplicaciones OLE DB existentes, el problema principal es si necesita acceder a las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si su aplicación es antigua y no necesita las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede seguir usando WDAC. Pero si necesita acceder a esas características nuevas, como el [tipo de datos xml](../../t-sql/xml/xml-transact-sql.md), debe usar el controlador OLE DB para SQL Server.  
  
 Tanto OLE DB Driver for SQL Server como MDAC admiten el aislamiento de transacciones de lectura confirmada mediante las versiones de fila, pero solo OLE DB Driver for SQL Server admite el aislamiento de transacciones de instantáneas. (En términos de programación, el aislamiento de transacción de instantánea con versiones de fila es igual que la transacción de lectura confirmada).  
  
 Para información sobre las diferencias entre OLE DB Driver for SQL Server y MDAC, consulte [Actualización de una aplicación a OLE DB Driver for SQL Server desde MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
## <a name="see-also"></a>Consulte también  
 [Controlador OLE DB para SQL Server](oledb-driver-for-sql-server.md)  
 [Temas de procedimientos de OLE DB](ole-db-how-to/ole-db-how-to-topics.md)  
  
  
