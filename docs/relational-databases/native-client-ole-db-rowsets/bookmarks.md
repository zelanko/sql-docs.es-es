---
description: Marcadores de fila (proveedor de OLE DB de Native Client)
title: Marcadores de fila (proveedor de OLE DB de Native Client) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bookmarks [OLE DB]
- SQL Server Native Client OLE DB provider, bookmarks
- rowsets [OLE DB], bookmarks
- OLE DB rowsets, bookmarks
ms.assetid: 7d9076f2-bf9c-452e-b816-70371a0c1644
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e822cef42606e18334e1494006f7d28c3e8308b9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463466"
---
# <a name="bookmarks-in-sql-server-native-client"></a>Marcadores en SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Los marcadores permiten a los consumidores volver rápidamente a una fila. Gracias a los marcadores, los consumidores pueden tener acceso de forma aleatoria a las filas en función del valor de marcador. La columna de marcador es la columna 0 en el conjunto de filas. El consumidor establece el valor de campo dwFlag de la estructura de enlace en DBCOLUMNSINFO_ISBOOKMARK para indicar que la columna se utiliza de marcador. El consumidor establece también la propiedad de conjunto de filas DBPROP_BOOKMARKS en VARIANT_TRUE. Esto permite que la columna 0 esté presente en el conjunto de filas. Después, se usa el método **IRowsetLocate::GetRowsAt** para capturar las filas, empezando por la fila especificada como desplazamiento desde un marcador.  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
