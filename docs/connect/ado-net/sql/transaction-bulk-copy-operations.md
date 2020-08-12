---
title: Operaciones de transacción y de copia masiva
description: Describe cómo realizar una operación de copia masiva en una transacción, incluida la forma de confirmar o revertir la transacción.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f6f0cbc9-f7bf-4d6e-875f-ad1ba0b4aa62
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 685bb349366ad955248a05e23ec030788dcbc63d
ms.sourcegitcommit: 6b3569977b034554883a94d73d1c4df6e2f74fe2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2020
ms.locfileid: "85106915"
---
# <a name="transaction-and-bulk-copy-operations"></a>Operaciones de transacción y de copia masiva

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Las operaciones de copia masiva se pueden realizar como operaciones aisladas o como parte de una transacción en varios pasos. Esta última opción permite realizar más de una operación de copia masiva en la misma transacción, así como realizar otras operaciones de base de datos, tales como inserciones, actualizaciones y eliminaciones, mientras todavía se puede confirmar o revertir la transacción entera.  
  
De forma predeterminada, una operación de copia masiva se realiza como una operación aislada. La operación de copia masiva tiene lugar sin transacciones y sin la oportunidad de revertirla. Si necesita revertir parte de la copia masiva o la totalidad de esta cuando se produce un error, puede hacer lo siguiente:

 - Usar una transacción administrada por <xref:Microsoft.Data.SqlClient.SqlBulkCopy>

 - Realizar la operación de copia masiva en una transacción existente

 - Darla de alta en **System.Transactions** <xref:System.Transactions.Transaction>.  
  
## <a name="performing-a-non-transacted-bulk-copy-operation"></a>Realizar una operación de copia masiva sin transacciones  
La aplicación de consola siguiente muestra lo que sucede cuando una operación de copia masiva sin transacciones detecta un error en medio de la operación.  
  
En el ejemplo, las tablas de origen y de destino incluyen cada una una columna `Identity` denominada **ProductID**. En primer lugar, el código prepara la tabla de destino mediante la eliminación de todas las filas y luego inserta una sola fila cuyo **ProductID** se sabe que existe en la tabla de origen. De forma predeterminada, se genera un nuevo valor para la columna `Identity` en la tabla de destino para cada fila agregada. En este ejemplo, cuando se abre la conexión, se establece una opción que obliga al proceso de carga masiva a usar los valores `Identity` de la tabla de origen en su lugar.  
  
La operación de copia masiva se ejecuta con la propiedad <xref:Microsoft.Data.SqlClient.SqlBulkCopy.BatchSize%2A> establecida en 10. Cuando la operación encuentra la fila no válida, se produce una excepción. En este primer ejemplo, la operación de copia masiva es sin transacciones. Se confirman todos los lotes que se copian hasta el momento del error. El lote que contiene la clave duplicada se revierte y la operación de copia masiva se detiene antes de procesar los lotes restantes.  
  
> [!NOTE]
>  Este ejemplo no se ejecuta a menos que haya creado las tablas de trabajo como se describe en [Configuración de ejemplos de copia masiva](bulk-copy-example-setup.md). Este código se proporciona para mostrar la sintaxis para usar **SqlBulkCopy**. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción `INSERT … SELECT` de Transact-SQL para copiar los datos.  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_Default#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_Default.cs#1)]
  
## <a name="performing-a-dedicated-bulk-copy-operation-in-a-transaction"></a>Realización de una operación de copia masiva dedicada en una transacción  
De forma predeterminada, una operación de copia masiva es su propia transacción. Si quiere realizar una operación de copia masiva dedicada, cree una instancia de <xref:Microsoft.Data.SqlClient.SqlBulkCopy> con una cadena de conexión o use un objeto <xref:Microsoft.Data.SqlClient.SqlConnection> existente sin una transacción activa. La operación de copia masiva crea una transacción en cada escenario y luego la confirma o revierte.  
  
Puede especificar explícitamente la opción <xref:Microsoft.Data.SqlClient.SqlBulkCopyOptions.UseInternalTransaction> en el constructor de la clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy> para ejecutar una operación de copia masiva en su propia transacción. Cada lote de la operación se ejecutará en una transacción independiente.  
  
> [!NOTE]
>  Dado que diferentes lotes se ejecutan en diferentes transacciones, si se produce un error durante la operación de copia masiva, se revertirán todas las filas del lote actual, pero las filas de los lotes anteriores permanecerán en la base de datos.  
  
La aplicación de consola siguiente es similar al ejemplo anterior, con una excepción: en este caso, la operación de copia masiva administra sus propias transacciones. Se confirman todos los lotes que se copian hasta el momento del error. El lote que contiene la clave duplicada se revierte y la operación de copia masiva se detiene antes de procesar los lotes restantes. 
  
> [!IMPORTANT]
>  Este ejemplo no se ejecuta a menos que haya creado las tablas de trabajo como se describe en [Configuración de ejemplos de copia masiva](bulk-copy-example-setup.md). Este código se proporciona para mostrar la sintaxis para usar **SqlBulkCopy**. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción `INSERT … SELECT` de Transact-SQL para copiar los datos.  
  
[!code-csharp[DataWorks SqlBulkCopyOptions_UseInternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopyOptions_UseInternalTransaction.cs#1)]
  
## <a name="using-existing-transactions"></a>Uso de transacciones existentes  
Puede especificar un objeto <xref:Microsoft.Data.SqlClient.SqlTransaction> existente como un parámetro en un constructor de <xref:Microsoft.Data.SqlClient.SqlBulkCopy>. En esta situación, la operación de copia masiva se realiza en la transacción existente y no se realiza ningún cambio en el estado de dicha transacción. Es decir, no se confirma ni se anula. Este método permite que una aplicación incluya la operación de copia masiva en una transacción con otras operaciones de base de datos. Sin embargo, si no se especifica un objeto <xref:Microsoft.Data.SqlClient.SqlTransaction> y se pasa una referencia nula, y la conexión tiene una transacción activa, se produce una excepción.   
  
Si se produce un error y necesita revertir toda la operación de copia masiva, o si la copia masiva debe ejecutarse como parte de un proceso más grande que se pueda revertir, puede proporcionar un objeto <xref:Microsoft.Data.SqlClient.SqlTransaction> al constructor de <xref:Microsoft.Data.SqlClient.SqlBulkCopy>.  
  
La siguiente aplicación de consola es similar al primer ejemplo (sin transacciones), con una excepción: en este ejemplo, la operación de copia masiva se incluye en una transacción externa más grande. Cuando se produce la infracción de la clave principal, toda la transacción se revierte y no se agrega ninguna fila a la tabla de destino.  
  
> [!IMPORTANT]
>  Este ejemplo no se ejecuta a menos que haya creado las tablas de trabajo como se describe en [Configuración de ejemplos de copia masiva](bulk-copy-example-setup.md). Este código se proporciona para mostrar la sintaxis para usar **SqlBulkCopy**. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción `INSERT … SELECT` de Transact-SQL para copiar los datos.  
  
[!code-csharp[DataWorks SqlBulkCopy_ExternalTransaction#1](~/../sqlclient/doc/samples/SqlBulkCopy_ExternalTransaction.cs#1)]
  
## <a name="next-steps"></a>Pasos siguientes
- [Operaciones de copia masiva en SQL Server](bulk-copy-operations-sql-server.md)
