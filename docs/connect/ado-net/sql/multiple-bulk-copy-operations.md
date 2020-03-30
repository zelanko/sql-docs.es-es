---
title: Varias operaciones de copia masiva.
description: Describe cómo realizar varias operaciones de copia masiva de datos en una instancia de SQL Server mediante la clase SqlBulkCopy.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 5ad12f94-7459-4a93-a421-4160d1a90715
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: f052e70d55a789eab731f94ae086d2f47384593c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896581"
---
# <a name="multiple-bulk-copy-operations"></a>Varias operaciones de copia masiva.

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Puede realizar varias operaciones de copia masiva con una única instancia de una clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. Si los parámetros de operación cambian entre copias (por ejemplo, el nombre de la tabla de destino), debe actualizarlos antes de las subsiguientes llamadas a cualquiera de los métodos **WriteToServer**, como se muestra en el ejemplo siguiente. A menos que se cambien explícitamente, todos los valores de propiedad permanecen igual que estaban en la operación de copia masiva anterior para una instancia determinada.  
  
> [!NOTE]
>  Generalmente, es más eficaz realizar varias operaciones de copia masiva con la misma instancia de <xref:Microsoft.Data.SqlClient.SqlBulkCopy> que usar una instancia independiente para cada operación.  
  
Si se realizan varias operaciones de copia masiva con el mismo objeto <xref:Microsoft.Data.SqlClient.SqlBulkCopy>, no hay restricciones en cuanto a si la información de origen o destino es igual o diferente en cada operación. Sin embargo, debe asegurarse de que la información de asociación de la columna está establecida correctamente cada vez que se escribe en el servidor.  

## <a name="example"></a>Ejemplo

> [!IMPORTANT]
>  Este ejemplo no se ejecuta a menos que haya creado las tablas de trabajo como se describe en [Configuración de ejemplos de copia masiva](bulk-copy-example-setup.md). Este código se proporciona para mostrar la sintaxis para usar **SqlBulkCopy**. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción `INSERT … SELECT` de Transact-SQL para copiar los datos.  
  
[!code-csharp[DataWorks SqlBulkCopy_._ColumnMappingOrdersDetails#1](~/../sqlclient/doc/samples/SqlBulkCopy_ColumnMappingOrdersDetails.cs#1)]
  
## <a name="next-steps"></a>Pasos siguientes
- [Operaciones de copia masiva en SQL Server](bulk-copy-operations-sql-server.md)
