---
title: Actualización de datos en cursores de SQL Server | Microsoft Docs
description: Actualizar datos en cursores de SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
ms.openlocfilehash: e5ccf4831cf882eedd4b2b95894d44457402bb6e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994162"
---
# <a name="updating-data-in-sql-server-cursors"></a>Actualizar datos en cursores de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Cuando se capturan y actualizan datos mediante cursores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], las mismas consideraciones y restricciones que se aplican a cualquier otra aplicación cliente son válidas para una aplicación de consumidor del controlador OLE DB para SQL Server.  
  
 Solo las filas de cursores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] participan en el control del acceso simultáneo a datos. Cuando el consumidor solicita un conjunto de filas modificable, DBPROP_LOCKMODE controla el control de simultaneidad. Para modificar el nivel de control de acceso simultáneo, el consumidor establece la propiedad DBPROP_LOCKMODE antes de abrir el conjunto de filas.  
  
 Los niveles de aislamiento de las transacciones pueden producir diferencias significativas en la posición de las filas si el diseño de la aplicación cliente permite que las transacciones permanezcan abiertas durante largos períodos de tiempo. De forma predeterminada, el controlador OLE DB para SQL Server usa el nivel de aislamiento de lectura confirmada especificado por DBPROPVAL_TI_READCOMMITTED. OLE DB Driver for SQL Server admite el aislamiento de lectura de datos sucios cuando la simultaneidad del conjunto de filas es de solo lectura. Por consiguiente, el consumidor puede solicitar un nivel superior de aislamiento en un conjunto de filas modificable pero no puede solicitar con éxito un nivel inferior.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modos de actualización inmediata y retrasada  
 En el modo de actualización inmediata, cada llamada a **IRowsetChange::SetData** produce un recorrido de ida y vuelta a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si el consumidor realiza varios cambios en una única fila, resulta más eficaz enviar todos los cambios con una única llamada a **SetData**.  
  
 En el modo de actualización retrasada, se realiza un recorrido de ida y vuelta a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para cada fila indicada en los parámetros *cRows* y *rghRows* de **IRowsetUpdate::Update**.  
  
 En ambos modos, un viaje de ida y vuelta representa una transacción distinta cuando no queda abierto ningún objeto de transacción para el conjunto de filas.  
  
 Cuando se usa **IRowsetUpdate::Update**, OLE DB Driver for SQL Server intenta procesar cada una de las filas indicadas. Cuando se produce un error debido a valores de datos, longitud o estado no válidos en cualquier fila, el procesamiento del controlador OLE DB para SQL Server no se detiene. Se pueden modificar todas o ninguna de las demás filas que participan en la actualización. El consumidor debe examinar la matriz *prgRowStatus* devuelta para determinar el error que se haya podido producir en una fila concreta cuando el controlador OLE DB para SQL Server devuelve DB_S_ERRORSOCCURRED.  
  
 Un consumidor no debe suponer que las filas se procesan en un orden determinado. Si un consumidor necesita el procesamiento ordenado de modificación de datos en más de una fila, debe establecer ese orden en la lógica de la aplicación y abrir una transacción para incluir en ella el proceso.  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar datos en conjuntos de filas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
