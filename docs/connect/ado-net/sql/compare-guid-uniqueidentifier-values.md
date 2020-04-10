---
title: Comparación de valores GUID y uniqueidentifier
description: Muestra cómo trabajar con valores GUID y de identificador único en SQL Server y .NET.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: aababd75-2335-43e3-ace8-4b7ae84191a8
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 33f46c0a88acf88238cc92015e6a2858fa8765b8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928893"
---
# <a name="comparing-guid-and-uniqueidentifier-values"></a>Comparación de valores GUID y uniqueidentifier

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

El tipo de datos de identificador único global (GUID) de SQL Server se representa mediante el tipo de datos `uniqueidentifier`, que almacena un valor binario de 16 bytes. Un GUID es un número binario que sirve principalmente como identificador que debe ser único en una red formada por varios equipos en muchos sitios. Los GUID se pueden generar mediante una llamada a la función NEWID de Transact-SQL y se garantiza que sea único en todo el mundo. Para obtener más información, vea [uniqueidentifier (Transact-SQL)](../../../t-sql/data-types/uniqueidentifier-transact-sql.md).  
  
## <a name="working-with-sqlguid-values"></a>Uso de valores SqlGuid  
Dado que los valores de GUID son largos y poco claros, no son significativos para los usuarios. Si se usan GUID generados de forma aleatoria para los valores de clave e inserta una gran cantidad de filas, obtendrá E/S aleatoria en los índices, lo que puede afectar negativamente al rendimiento. Los GUID también son relativamente grandes en comparación con otros tipos de datos. En general, se recomienda usar GUID solo para escenarios muy estrechos en los que no sea adecuado ningún otro tipo de datos.  
  
### <a name="comparing-guid-values"></a>Comparación de valores de GUID  
Con los valores `uniqueidentifier` se pueden usar operadores de comparación. No obstante, no se implementa la ordenación mediante la comparación de los patrones de bits de los dos valores. Las únicas operaciones que se permiten con respecto a un valor `uniqueidentifier` son las comparaciones (=, <>, \<, >, \<=, >=) y la comprobación de NULL (IS NULL e IS NOT NULL). No se permite ningún otro operador aritmético.  
  
Tanto <xref:System.Guid> como <xref:System.Data.SqlTypes.SqlGuid> tienen un método `CompareTo` para comparar distintos valores GUID. Sin embargo, `System.Guid.CompareTo` y `SqlTypes.SqlGuid.CompareTo` se implementan de forma diferente. <xref:System.Data.SqlTypes.SqlGuid> implementa `CompareTo` con el comportamiento de SQL Server, los seis últimos bytes de un valor son más significativos. <xref:System.Guid> evalúa los 16 bytes. En el ejemplo siguiente se muestra esta diferencia de comportamiento. La primera sección del código muestra los valores de <xref:System.Guid> sin ordenar y la segunda sección de código muestra los valores de <xref:System.Guid> ordenados. En la tercera sección se muestran los valores de <xref:System.Data.SqlTypes.SqlGuid> ordenados. El resultado se muestra debajo de la lista de códigos.  
  
[!code-csharp[DataWorks SqlGuid#1](~/../sqlclient/doc/samples/SqlGuid.cs#1)]
  
Este ejemplo genera los siguientes resultados.  
  
```console
Unsorted Guids:  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
  
Sorted Guids:  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
  
Sorted SqlGuids:  
2aaaaaaa-bbbb-cccc-dddd-1eeeeeeeeeee  
3aaaaaaa-bbbb-cccc-dddd-2eeeeeeeeeee  
1aaaaaaa-bbbb-cccc-dddd-3eeeeeeeeeee  
```  
  
## <a name="next-steps"></a>Pasos siguientes
- [Tipos de datos de SQL Server en ADO.NET](sql-server-data-types.md)
