---
title: Operaciones por lotes con objetos DataAdapter
description: Se describe la mejora del rendimiento de la aplicación mediante la reducción del número de recorridos de ida y vuelta a SQL Server al aplicar actualizaciones desde el objeto DataSet.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: e72ed5af-b24f-486c-8429-c8fd2208f844
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 1b720dff0678c68396fe7d8cf1f60f3ade70dd9d
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772335"
---
# <a name="batch-operations-using-dataadapters"></a>Operaciones por lotes con objetos DataAdapter

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

La compatibilidad con las operaciones por lotes en ADO.NET permite que un <xref:System.Data.Common.DataAdapter> agrupe operaciones INSERT, UPDATE y DELETE desde un <xref:System.Data.DataSet> o una <xref:System.Data.DataTable> al servidor, en lugar de enviar las operaciones de una en una. La reducción del número de viajes de ida y vuelta (round trip) al servidor tiene como resultado una mejora considerable del rendimiento. Se admite la actualización por lotes para el proveedor de datos SqlClient de Microsoft para SQL Server (<xref:Microsoft.Data.SqlClient>).

Al actualizar una base de datos con modificaciones de un <xref:System.Data.DataSet> en versiones anteriores de ADO.NET, el método `Update` de un `DataAdapter` realizaba actualizaciones de las filas de la base de datos de una en una. A medida que recorría las filas de la <xref:System.Data.DataTable> especificada, examinaba cada <xref:System.Data.DataRow> para ver si se había modificado. Si se había modificado la fila, llamaba al `UpdateCommand`, `InsertCommand` o `DeleteCommand` apropiado, en función del valor de propiedad <xref:System.Data.DataRow.RowState%2A> de la fila. Cada actualización de una fila implicaba un viaje de ida y vuelta (round trip) a la base de datos.

En el proveedor de datos SqlClient de Microsoft para SQL Server, <xref:Microsoft.Data.SqlClient.SqlDataAdapter> expone una propiedad <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateBatchSize%2A>. Si se establece el `UpdateBatchSize` en un valor entero positivo, se producen actualizaciones en la base de datos que se envían como lotes del tamaño especificado. Por ejemplo, si se establece el `UpdateBatchSize` en 10, se agrupan 10 instrucciones separadas y se envían en un único lote. Si se establece el `UpdateBatchSize` en 0, el <xref:Microsoft.Data.SqlClient.SqlDataAdapter> utilizará el mayor tamaño de lote admitido por el servidor. Si se establece el valor en 1, se deshabilitan las actualizaciones por lotes y las filas se envían de una en una.

> [!NOTE]
> Si se ejecuta un lote demasiado grande, el rendimiento podría verse afectado. Por tanto, es conveniente realizar pruebas a fin de determinar el valor óptimo del tamaño del lote antes de implementar la aplicación.

## <a name="use-the-updatebatchsize-property"></a>Uso de la propiedad UpdateBatchSize

Al habilitar las actualizaciones por lotes, el valor de propiedad <xref:System.Data.IDbCommand.UpdatedRowSource%2A> de `UpdateCommand`, `InsertCommand` y `DeleteCommand` del DataAdapter debe establecerse en <xref:System.Data.UpdateRowSource.None> o <xref:System.Data.UpdateRowSource.OutputParameters>. Al realizar una actualización por lotes, el valor <xref:System.Data.IDbCommand.UpdatedRowSource%2A> o <xref:System.Data.UpdateRowSource.FirstReturnedRecord> de la propiedad <xref:System.Data.UpdateRowSource.Both> del comando no es válido.
  
En el siguiente procedimiento se muestra cómo se utiliza la propiedad `UpdateBatchSize`. En el procedimiento se toman dos argumentos, un objeto <xref:System.Data.DataSet> con columnas que representan los campos **ProductCategoryID** y **Name** de la tabla **Production.ProductCategory**, y un entero que representa el tamaño del lote (el número de filas). El código crea un objeto <xref:Microsoft.Data.SqlClient.SqlDataAdapter> nuevo y se establecen las propiedades <xref:Microsoft.Data.SqlClient.SqlDataAdapter.UpdateCommand%2A>, <xref:Microsoft.Data.SqlClient.SqlDataAdapter.InsertCommand%2A> y <xref:Microsoft.Data.SqlClient.SqlDataAdapter.DeleteCommand%2A>. En el código se supone que el objeto <xref:System.Data.DataSet> tiene filas modificadas. Se establece la propiedad `UpdateBatchSize` y se ejecuta la actualización.

[!code-csharp[SqlDataAdapter_Batch#1](~/../sqlclient/doc/samples/SqlDataAdapter_Batch.cs#1)]

## <a name="handle-batch-update-related-events-and-errors"></a>Control de errores y eventos relacionados con la actualización por lotes

**DataAdapter** tiene dos eventos relacionados con la actualización: **RowUpdating** y **RowUpdated**. Para obtener más información, vea [Control de eventos de objetos DataAdapter](handle-dataadapter-events.md).

### <a name="event-behavior-changes-with-batch-updates"></a>Cambios de comportamiento de eventos con actualizaciones por lotes

Si se habilita el procesamiento por lotes, se actualizan varias filas en una única operación de base de datos. Por tanto, solo se produce un evento `RowUpdated` para cada lote, mientras que el evento `RowUpdating` se produce para cada fila procesada. Si se deshabilita el procesamiento por lotes, los dos eventos se activan con entrelazado individualizado, donde los eventos `RowUpdating` y `RowUpdated` se activan para una fila y, a continuación, se activan los eventos `RowUpdating` y `RowUpdated` para la siguiente fila, hasta que se hayan procesado todas las filas.

### <a name="access-updated-rows"></a>Acceso a filas actualizadas

Si se deshabilita el procesamiento por lotes, se puede obtener acceso a la fila que se está actualizando mediante la propiedad <xref:System.Data.Common.RowUpdatedEventArgs.Row%2A> de la clase <xref:System.Data.Common.RowUpdatedEventArgs>.

Cuando se habilita el procesamiento por lotes, se genera un único evento `RowUpdated` para varias filas. Por tanto, el valor de la propiedad `Row` para cada fila es nulo. Aún así, los eventos `RowUpdating` se generarán para cada fila. El método <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A> de la clase <xref:System.Data.Common.RowUpdatedEventArgs> permite obtener acceso a las filas procesadas al copiar referencias a las mismas en una matriz. Si no se está procesando ninguna fila, `CopyToRows` inicia una <xref:System.ArgumentNullException>. Utilice la propiedad <xref:System.Data.Common.RowUpdatedEventArgs.RowCount%2A> para devolver el número de filas procesadas antes de llamar al método <xref:System.Data.Common.RowUpdatedEventArgs.CopyToRows%2A>.

### <a name="handle-data-errors"></a>Control de errores de datos

La ejecución por lotes tiene el mismo efecto que la ejecución de cada instrucción por separado. Las instrucciones se ejecutan en el mismo orden en el que se agregaron al lote. Los errores se controlan de la misma forma en el modo de procesamiento por lotes que cuando éste se encuentra deshabilitado. Cada fila se procesa por separado. Solo aquellas filas procesadas correctamente en la base de datos se actualizarán en la <xref:System.Data.DataRow> correspondiente dentro de la <xref:System.Data.DataTable>.

> [!NOTE]
> El proveedor de datos SqlClient de Microsoft SQL Server y el servidor de base de datos de back-end determinan qué construcciones SQL se admiten para la ejecución por lotes. Es posible que se inicie una excepción si se envía una instrucción no compatible para su ejecución.

## <a name="see-also"></a>Consulte también

- [Objetos DataAdapter y DataReader](dataadapters-datareaders.md)
- [Actualización de orígenes de datos con objetos DataAdapter](update-data-sources-with-dataadapters.md)
- [Control de eventos de objetos DataAdapter](handle-dataadapter-events.md)
- [Microsoft ADO.NET para SQL Server](microsoft-ado-net-sql-server.md)
