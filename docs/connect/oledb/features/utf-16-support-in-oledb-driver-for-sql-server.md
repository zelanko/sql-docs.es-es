---
title: Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server | Documentos de Microsoft
description: Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: f88dea7bbc4fbd2ea6307647e1cbce47b07a0558
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], si se proporciona un búfer de longitud fija al enlazar un parámetro de resultado o salida de la columna y si la **wchar** carácter escrito en el búfer antes de que el carácter de terminación es un punto de código suplente alto de un suplentes par y si la siguiente **wchar** carácter es un punto de código suplente bajo, el controlador OLE DB para SQL Server no agregará el punto de código suplente alto en el búfer.  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
