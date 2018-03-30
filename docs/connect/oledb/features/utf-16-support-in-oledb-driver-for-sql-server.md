---
title: Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server | Documentos de Microsoft
description: Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f4e1103b25deb46d03ce26a79ba3649305c283d
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], si se proporciona un búfer de longitud fija al enlazar un parámetro de resultado o salida de la columna y si la **wchar** carácter escrito en el búfer antes de que el carácter de terminación es un punto de código suplente alto de un suplentes par y si la siguiente **wchar** carácter es un punto de código suplente bajo, el controlador OLE DB para SQL Server no agregará el punto de código suplente alto en el búfer.  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
