---
title: Resincronización de filas | Microsoft Docs
description: Resincronización de filas mediante OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2f1ea1a563e986914c5fe820740776da129c3b28
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994175"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>Actualizar datos en conjuntos de filas: volver a sincronizar filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server admite **IRowsetResynch** en conjuntos de filas compatibles con cursores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **IRowsetResynch** no está disponible a petición. El consumidor debe solicitar la interfaz antes de abrir el conjunto de filas.  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar datos en conjuntos de filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
