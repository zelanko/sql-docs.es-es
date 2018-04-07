---
title: Cuándo se debe utilizar el controlador OLE DB para SQL Server | Documentos de Microsoft
description: Cuándo se debe utilizar el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 361a13bd249bef726e202fc8fef69fb48d88b746
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>Cuándo se debe utilizar el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Controlador de OLE DB para SQL Server es una tecnología que puede utilizar para tener acceso a datos en un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de datos.  Para obtener una explicación de las tecnologías de acceso a datos diferentes, consulte [mapa de carreteras de tecnologías de acceso de datos](http://go.microsoft.com/fwlink/?LinkID=179186)  
  
 Al decidir si desea usar el controlador OLE DB para SQL Server como la tecnología de acceso a datos de la aplicación, debe tener en cuenta varios factores.  
  
 En el caso aplicaciones nuevas, si está utilizando un lenguaje de programación administrado, como Microsoft Visual C# o Visual Basic, y necesita obtener acceso a las nuevas características introducidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debería utilizar el proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que forma parte de .NET Framework.  
  
 Si está desarrollando una aplicación basada en COM y necesita obtener acceso a las nuevas características introducidas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe usar el controlador OLE DB para SQL Server. Si no necesita obtener acceso a las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede seguir utilizando Windows Data Access Components (WDAC).  
  
 Para las aplicaciones existentes de OLE DB, el problema principal es si necesita tener acceso a las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si su aplicación es antigua y no necesita las nuevas características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], puede seguir usando WDAC. Sin embargo, si es necesario tener acceso a esas características nuevas, como el [tipo de datos xml](../../t-sql/xml/xml-transact-sql.md), debe usar el controlador OLE DB para SQL Server.  
  
 Ambos controlador OLE DB para SQL Server como MDAC admiten el aislamiento de transacción confirmada mediante las versiones de fila, pero sólo controlador OLE DB para el aislamiento de transacción de instantánea de SQL Server admite de lectura. (En términos de programación, el aislamiento de transacción de instantánea con versiones de fila es igual que la transacción de lectura confirmada).  
  
 Para obtener información sobre las diferencias entre el controlador OLE DB para SQL Server y MDAC, consulte [actualizar una aplicación a controlador de OLE DB para SQL Server de MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para la programación de SQL Server](../oledb/oledb-driver-for-sql-server-programming.md)     
 [Temas "Cómo..." de OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
