---
title: Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server | Documentos de Microsoft
description: Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: bcb7393315063102315fdf5062bdfa05ee07282d
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/14/2018
ms.locfileid: "35611630"
---
# <a name="utf-16-support-in-ole-db-driver-for-sql-server"></a>Compatibilidad con UTF-16 en el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], si se proporciona un búfer de longitud fija al enlazar un parámetro de resultado o salida de la columna y si la **wchar** carácter escrito en el búfer antes de que el carácter de terminación es un punto de código suplente alto de un suplentes par y si la siguiente **wchar** carácter es un punto de código suplente bajo, el controlador OLE DB para SQL Server no agregará el punto de código suplente alto en el búfer.  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
  
  
