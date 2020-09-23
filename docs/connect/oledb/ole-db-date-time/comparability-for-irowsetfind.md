---
title: Comparabilidad de IRowsetFind | Microsoft Docs
description: Obtenga información sobre las comparaciones que IRowsetFind admite para los tipos de fecha/hora en OLE DB Driver for SQL Server. DB_E_BADCOMPAREOP se devuelve para otras comparaciones.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IRowsetFind comparability
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16ef589a18c2be5317157e7db5790af06c8c613a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861405"
---
# <a name="comparability-for-irowsetfind"></a>Comparaciones en IRowsetFind
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  IRowsetFind admite las comparaciones siguientes para los tipos de fecha y hora únicamente:  
  
-   LT  
  
-   LE  
  
-   EQ  
  
-   GE  
  
-   GT  
  
-   NE  
  
-   IGNORE  
  
 Si se intenta realizar cualquier otra comparación, se obtiene DB_E_BADCOMPAREOP. Esto es coherente con la especificación OLE DB.  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
