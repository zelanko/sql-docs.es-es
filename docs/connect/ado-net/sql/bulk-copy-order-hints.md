---
title: Sugerencias de orden para operaciones de copia masiva
description: Describe cómo usar las sugerencias de orden en las operaciones de copia masiva.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: c7365bdc6da75e04d019ca1a6a87b90dd8d4ec3c
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85110186"
---
# <a name="order-hints-for-bulk-copy-operations"></a>Sugerencias de orden para operaciones de copia masiva

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Las operaciones de copia masiva ofrecen importantes ventajas de rendimiento con respecto a otros métodos a la hora de cargar datos en una tabla de SQL Server. El rendimiento se puede mejorar aún más mediante el uso de sugerencias de orden. Al especificar sugerencias de orden para las operaciones de copia masiva se puede reducir el tiempo de inserción de los datos ordenados en tablas con índices agrupados.

De forma predeterminada, la operación de inserción masiva presupone que los datos entrantes no están ordenados. SQL Server fuerza una ordenación intermedia de estos datos antes de cargarlos de forma masiva. Si sabe que los datos entrantes ya están ordenados, puede utilizar las sugerencias de orden para indicar a la operación de copia masiva el criterio de ordenación de las columnas de destino que forman parte de un índice agrupado.
  
## <a name="adding-order-hints-to-a-bulk-copy-operation"></a>Agregar sugerencias de orden a una operación de copia masiva  
En el ejemplo siguiente se copian de forma masiva datos de una tabla de origen en la base de datos de ejemplo **AdventureWorks** a una tabla de destino en la misma base de datos. Se crea un objeto SqlBulkCopyColumnOrderHint para definir el criterio de ordenación de la columna **ProductNumber** en la tabla de destino. Después, se agrega la sugerencia de orden a la instancia de SqlBulkCopy, que anexará el argumento de sugerencia de orden adecuado a la consulta de `INSERT BULK` resultante.

[!code-csharp [SqlBulkCopy.ColumnOrderHint#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnOrderHint.cs#1)]

## <a name="next-steps"></a>Pasos siguientes
- [Operaciones de copia masiva en SQL Server](bulk-copy-operations-sql-server.md)
