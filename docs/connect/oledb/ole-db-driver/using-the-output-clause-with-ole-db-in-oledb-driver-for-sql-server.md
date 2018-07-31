---
title: Uso de la cláusula OUTPUT con OLE DB en el controlador OLE DB para SQL Server | Microsoft Docs
description: Uso de la cláusula OUTPUT con OLE DB en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ad3408d0419e408809b151114d83a09d976505fa
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109397"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>Uso de la cláusula OUTPUT con OLE DB en el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Si utiliza una cláusula OUTPUT en un comando INSERT, UPDATE, DELETE o MERGE, no estará disponible el recuento de filas afectadas. La aplicación debe contar el número de filas del conjunto de filas que devuelve la cláusula OUTPUT.  
  
## <a name="see-also"></a>Ver también  
 [Creación de un controlador OLE DB para la aplicación de SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
