---
title: Uso de la cláusula OUTPUT con OLE DB en el controlador OLE DB para SQL Server | Microsoft Docs
description: Uso de la cláusula OUTPUT con OLE DB en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 3ca08ca3439c2dde50cb4a7a1226688854fd6fe0
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994970"
---
# <a name="using-the-output-clause-with-ole-db-in-ole-db-driver-for-sql-server"></a>Uso de la cláusula OUTPUT con OLE DB en el controlador de OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Si utiliza una cláusula OUTPUT en un comando INSERT, UPDATE, DELETE o MERGE, no estará disponible el recuento de filas afectadas. La aplicación debe contar el número de filas del conjunto de filas que devuelve la cláusula OUTPUT.  
  
## <a name="see-also"></a>Consulte también  
 [Creación de un controlador OLE DB para la aplicación de SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md) 
  
  
