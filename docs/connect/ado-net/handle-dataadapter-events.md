---
title: Control de eventos de objetos DataAdapter
description: Se describen los eventos de DataAdapter y cómo usarlos.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 11515b25-ee49-4b1d-9294-a142147c1ec5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e3715f2060857bf6d5fabb37c049d6e9cff1ee40
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/16/2020
ms.locfileid: "97559217"
---
# <a name="handle-dataadapter-events"></a>Control de eventos de objetos DataAdapter

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

El proveedor de datos SqlClient de Microsoft para SQL Server <xref:Microsoft.Data.SqlClient.SqlDataAdapter> expone tres eventos que puede usar para responder a los cambios realizados en los datos en el origen de datos. En la siguiente tabla se muestran los eventos de `DataAdapter`.

|Evento|Descripción|  
|-----------|-----------------|  
|`RowUpdating`|Está a punto de comenzar una operación UPDATE, INSERT o DELETE en una fila (mediante una llamada a uno de los métodos `Update`).|  
|`RowUpdated`|Se ha completado una operación UPDATE, INSERT o DELETE en una fila (mediante una llamada a uno de los métodos `Update`).|  
|`FillError`|Se ha producido un error durante una operación `Fill`.|  

## <a name="rowupdating-and-rowupdated-events"></a>Eventos RowUpdating y RowUpdated

El evento `RowUpdating` se activa antes de que se produzca la actualización de una fila del <xref:System.Data.DataSet> en el origen de datos. El evento `RowUpdated` se activa después de que se produzca la actualización de una fila del `DataSet` en el origen de datos. Por lo tanto, puede utilizar `RowUpdating` para modificar el comportamiento de la actualización antes de que tenga lugar, proporcionar un control adicional del proceso durante la actualización, conservar una referencia a la fila actualizada, cancelar la actualización actual y programarla como parte de un proceso por lotes que se ejecutará después, entre otras acciones. `RowUpdated` es útil para reaccionar cuando se producen errores y excepciones durante la actualización. Puede agregar **información de error** a `DataSet`, así como **lógica de reintento**, etc.

Los argumentos <xref:System.Data.Common.RowUpdatingEventArgs> y <xref:System.Data.Common.RowUpdatedEventArgs> que se pasan a los eventos `RowUpdating` y `RowUpdated` incluyen lo siguiente: una propiedad `Command` que hace referencia al objeto `Command` que se está utilizando para realizar la actualización; una propiedad `Row` que hace referencia al objeto `DataRow` que contiene la información actualizada; una propiedad `StatementType` para el tipo de actualización que se está llevando a cabo; el valor de `TableMapping`, si es pertinente y el valor de `Status` de la operación.

Puede utilizar la propiedad `Status` para determinar si se ha producido o no un error durante la operación y, si lo desea, controlar las acciones que se emprenden en las filas actuales y las resultantes de la operación. Cuando se produce el evento, la propiedad `Status` toma el valor `Continue` o `ErrorsOccurred`. En la tabla siguiente se muestran los valores que se pueden asignar a la propiedad `Status` para controlar las acciones posteriores en el proceso de actualización.

|Situación|Descripción|  
|------------|-----------------|  
|`Continue`|Continuar la operación de actualización.|  
|`ErrorsOccurred`|Anular la operación de actualización e iniciar una excepción.|  
|`SkipCurrentRow`|Omitir la fila actual y continuar la operación de actualización.|  
|`SkipAllRemainingRows`|Anular la operación de actualización sin iniciar una excepción.|  

Al establecer a la propiedad `Status` en el valor `ErrorsOccurred` se inicia una excepción. Puede controlar qué excepciones se inician si establece la propiedad `Errors` en la excepción que desee. El uso de un valor distinto para la propiedad `Status` evita que se inicie una excepción.

También puede utilizar la propiedad `ContinueUpdateOnError` para controlar los errores producidos en las filas actualizadas. Cuando `DataAdapter.ContinueUpdateOnError` tiene el valor `true` y la actualización de una fila inicia una excepción, el texto de la excepción se coloca en la información `RowError` de la fila en cuestión y el proceso continúa sin que se inicie una excepción. De esta forma, puede responder a los errores cuando se complete el proceso `Update`, a diferencia del evento `RowUpdated`, que permite responder a los errores cuando se detectan.

En el ejemplo de código siguiente se muestra cómo se pueden agregar y quitar controladores de eventos. El controlador de eventos `RowUpdating` mantiene un registro de todos los registros eliminados y una marca de tiempo asociada a cada uno de ellos. El controlador de eventos `RowUpdated` agrega información de error a la propiedad `RowError` de la fila en `DataSet`, suprime la excepción y deja continuar el procesamiento (similar al comportamiento de `ContinueUpdateOnError` = `true`).

[!code-csharp[SqlDataAdapter_Events#1](~/../sqlclient/doc/samples/SqlDataAdapter_Events.cs#1)]

## <a name="fillerror-event"></a>FillError (evento)

Cuando se produce un error durante una operación `DataAdapter`, el objeto `FillError` provoca el evento `Fill`. Este tipo de error se suele producir cuando los datos de la fila que se agrega no se pueden convertir a un tipo de .NET sin cierta pérdida de precisión.

Si el error se produce durante una operación `Fill`, la fila actual no se agrega al objeto `DataTable`. El evento `FillError` permite resolver el error y agregar la fila o bien pasar por alto la fila excluida y continuar con la operación `Fill`.

El objeto <xref:System.Data.FillErrorEventArgs> que se pasa al evento `FillError` puede contener varias propiedades que permiten reaccionar en caso de errores y resolverlos. En la tabla siguiente se muestran las propiedades del objeto `FillErrorEventArgs`.

|Propiedad|Descripción|  
|--------------|-----------------|  
|`Errors`|`Exception` que se ha producido.|  
|`DataTable`|Objeto `DataTable` que se estaba llenando cuando ocurrió el error.|  
|`Values`|Matriz de objetos que contiene los valores de la fila que se está agregando cuando se produce el error. Las referencias de orden de la matriz `Values` coinciden con las de las columnas de la fila que se está agregando. Por ejemplo, `Values[0]` es el valor que se agrega en la primera columna de la fila.|  
|`Continue`|Permite elegir si desea iniciar una excepción o no. Si establece la propiedad `Continue` en `false`, la operación `Fill` en curso se detiene y se inicia una excepción. Si establece la propiedad `Continue` en `true`, la operación `Fill` continúa pese al error.|  

En el siguiente ejemplo de código se agrega un controlador para el evento `FillError` del objeto `DataAdapter`. En el código del evento `FillError`, el ejemplo determina si hay una posible pérdida de precisión y ofrece la posibilidad de reaccionar ante la excepción.

[!code-csharp[SqlDataAdapter_Events#2](~/../sqlclient/doc/samples/SqlDataAdapter_Events.cs#2)]

## <a name="see-also"></a>Consulte también

- [Objetos DataAdapter y DataReader](dataadapters-datareaders.md)
- [Eventos](/dotnet/standard/events/index)
- [Microsoft ADO.NET para SQL Server](microsoft-ado-net-sql-server.md)
