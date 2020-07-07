---
title: Actualización de datos en cursores de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
ms.assetid: 732dafee-f2d5-4aef-aad7-3a8bf3b1e876
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5627da0643b35bac430e59d9cbc0685ac6f44e38
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86013084"
---
# <a name="updating-data-in-sql-server-cursors"></a>Actualizar datos en cursores de SQL Server
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Al capturar y actualizar datos a través de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores, una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicación de consumidor de proveedor de OLE DB de cliente nativa está limitada por las mismas consideraciones y restricciones que se aplican a cualquier otra aplicación cliente.  
  
 Solo las filas de cursores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] participan en el control del acceso simultáneo a datos. Cuando el consumidor solicita un conjunto de filas modificable, DBPROP_LOCKMODE controla el control de simultaneidad. Para modificar el nivel de control de acceso simultáneo, el consumidor establece la propiedad DBPROP_LOCKMODE antes de abrir el conjunto de filas.  
  
 Los niveles de aislamiento de las transacciones pueden producir diferencias significativas en la posición de las filas si el diseño de la aplicación cliente permite que las transacciones permanezcan abiertas durante largos períodos de tiempo. De forma predeterminada, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client utiliza el nivel de aislamiento de lectura confirmada especificado por DBPROPVAL_TI_READCOMMITTED. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite el aislamiento de lectura Dirty cuando la simultaneidad del conjunto de filas es de solo lectura. Por consiguiente, el consumidor puede solicitar un nivel superior de aislamiento en un conjunto de filas modificable pero no puede solicitar con éxito un nivel inferior.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modos de actualización inmediata y retrasada  
 En el modo de actualización inmediata, cada llamada a **IRowsetChange::SetData** produce un recorrido de ida y vuelta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si el consumidor realiza varios cambios en una única fila, resulta más eficaz enviar todos los cambios con una única llamada a **SetData**.  
  
 En el modo de actualización retrasada, se realiza un recorrido de ida y vuelta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada fila indicada en los parámetros *cRows* y *rghRows* de **IRowsetUpdate::Update**.  
  
 En ambos modos, un viaje de ida y vuelta representa una transacción distinta cuando no queda abierto ningún objeto de transacción para el conjunto de filas.  
  
 Cuando se usa **IRowsetUpdate:: Update**, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client intenta procesar cada fila indicada. Se produce un error debido a que los valores de estado, longitud o datos no válidos de una fila no detienen el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procesamiento de proveedor de OLE DB de cliente nativo. Se pueden modificar todas o ninguna de las demás filas que participan en la actualización. El consumidor debe examinar la matriz *prgRowStatus* devuelta para determinar el error de cualquier fila concreta cuando el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client devuelve DB_S_ERRORSOCCURRED.  
  
 Un consumidor no debe suponer que las filas se procesan en un orden determinado. Si un consumidor necesita el procesamiento ordenado de modificación de datos en más de una fila, debe establecer ese orden en la lógica de la aplicación y abrir una transacción para incluir en ella el proceso.  
  
## <a name="see-also"></a>Consulte también  
 [Actualizar datos en conjuntos de filas](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
