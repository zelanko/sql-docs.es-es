---
title: Marcadores | Documentos de Microsoft
description: Marcadores en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- OLE DB Driver for SQL Server, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: f68094ae16436adf4268c65ec932235fb2fe647b
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689778"
---
# <a name="bookmarks"></a>Marcadores
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Marcadores permiten a los consumidores volver rápidamente a una fila. Gracias a los marcadores, los consumidores pueden tener acceso de forma aleatoria a las filas en función del valor de marcador. La columna de marcador es la columna 0 en el conjunto de filas. El consumidor establece el valor de campo dwFlag de la estructura de enlace en DBCOLUMNSINFO_ISBOOKMARK para indicar que la columna se utiliza de marcador. El consumidor establece también la propiedad de conjunto de filas DBPROP_BOOKMARKS en VARIANT_TRUE. Esto permite que la columna 0 esté presente en el conjunto de filas. El **IRowsetLocate:: GetRowsAt** método, a continuación, se utiliza para capturar filas, a partir de la fila especificada como un desplazamiento de un marcador.  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
