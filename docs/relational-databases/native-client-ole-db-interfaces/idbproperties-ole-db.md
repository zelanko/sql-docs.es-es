---
description: IDBProperties (proveedor de OLE DB de Native Client)
title: IDBProperties (proveedor de OLE DB de Native Client) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d8b1e72d69d047f2fee77db933f9acb447724035
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866744"
---
# <a name="idbproperties-native-client-ole-db-provider"></a>IDBProperties (proveedor de OLE DB de Native Client)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  La especificación estándar OLE DB permite a los proveedores especificar VT_EMPTY para **DBPROPINFO::vValues**. Sin embargo, OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client siempre devuelve VT_EMPTY cuando se llama a **IDBProperties::GetPropertyInfo** con **DBPROPSET_ROWSETALL** para recuperar propiedades de conjuntos de filas.  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](./sql-server-native-client-ole-db-interfaces.md)  
  
