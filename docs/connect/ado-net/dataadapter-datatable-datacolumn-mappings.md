---
title: Asignaciones de objetos DataAdapter, DataTable y DataColumn
description: Se describe cómo configurar DataTableMappings y ColumnMappings para un objeto DataAdapter.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e8b2f84fbbf888fc67cdb8f945d7f0c887c14eaa
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772324"
---
# <a name="dataadapter-datatable-and-datacolumn-mappings"></a>Asignaciones de objetos DataAdapter, DataTable y DataColumn

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Un objeto <xref:Microsoft.Data.SqlClient.SqlDataAdapter> contiene una colección con cero o más objetos <xref:System.Data.Common.DataTableMapping> en su propiedad <xref:System.Data.Common.DataAdapter.TableMappings%2A>. Un objeto **DataTableMapping** proporciona una asignación principal entre los datos devueltos por una consulta realizada en un origen de datos y una instancia de <xref:System.Data.DataTable>. El nombre de **DataTableMapping** se puede pasar en lugar del nombre de **DataTable** al método <xref:System.Data.Common.DbDataAdapter.Fill%2A> del objeto **DataAdapter**. En el ejemplo siguiente se crea un objeto **DataTableMapping** denominado **AuthorsMapping** en la tabla **Authors**.

```csharp
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");
```

Un objeto **DataTableMapping** permite usar en un objeto **DataTable** nombres de columna distintos a los de la base de datos. El objeto **DataAdapter** usa la asignación para hacer coincidir las columnas al actualizar la tabla.

> [!NOTE]
> Si no se especifica un nombre de **TableName** o **DataTableMapping** al llamar a los métodos **Fill** o **Update** del objeto **DataAdapter**, **DataAdapter** busca un objeto **DataTableMapping** denominado "Table". Si no existe ese objeto **DataTableMapping**, el valor **TableName** de **DataTable** es "Table". Puede especificar un objeto **DataTableMapping** predeterminado si crea una instancia de **DataTableMapping** con el nombre "Table".

En el ejemplo de código siguiente se crea un objeto **DataTableMapping** (del espacio de nombres <xref:System.Data.Common>) y, al asignarle el nombre "Table", se convierte en la asignación predeterminada del objeto **DataAdapter** especificado. Después, en el ejemplo se asignan las columnas de la primera tabla de los resultados de la consulta (la tabla **Customers** de la base de datos **Northwind**) a un conjunto de nombres más descriptivos existentes en la tabla **Northwind Customers** de <xref:System.Data.DataSet>. En las columnas que no se asignan se usa el nombre de la columna en el origen de datos.

[!code-csharp[SqlDataAdapter_TableMappings#1](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#1)]

En situaciones más avanzadas, podría decidir que quiere que el mismo objeto **DataAdapter** permita la carga de otras tablas con otras asignaciones. Para ello, agregue más objetos **DataTableMapping**.

Cuando al método **Fill** se le pasa una instancia de un objeto **DataSet** y un nombre de **DataTableMapping**, se usa una asignación con ese nombre, si existe, o bien un objeto **DataTable** con ese nombre.

En los ejemplos siguientes se crea un objeto **DataTableMapping** denominado **Customers** y un objeto **DataTable** con el nombre **BizTalkSchema**. Después, en el ejemplo se asignan las filas devueltas por la instrucción SELECT al objeto **DataTable** **BizTalkSchema**.

[!code-csharp[SqlDataAdapter_TableMappings#2](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#2)]

> [!NOTE]
> Si no se proporciona un nombre de columna de origen para una asignación de columnas, se generarán nombres predeterminados de forma automática. Si no se proporciona una columna de origen para una asignación de columnas, la asignación de columnas recibe un nombre predeterminado secuencial de **SourceColumn** *N*, comenzando por **SourceColumn1**.

> [!NOTE]
> Si no se proporciona un nombre de tabla de origen para una asignación de tabla, se generarán nombres predeterminados de forma automática. Si no se proporciona un nombre de tabla de origen para una asignación de tablas, la asignación de tablas recibe un nombre predeterminado secuencial de **SourceTable** *N*, comenzando por **SourceTable1**.

> [!NOTE]
> Es recomendable evitar la convención de nomenclatura de **SourceColumn** *N* para una asignación de columnas, o bien de **SourceTable** *N* para una asignación de tablas, ya que es posible que el nombre proporcionado entre en conflicto con el nombre predeterminado de asignación de columnas de **ColumnMappingCollection** o con el nombre de asignación de tablas de **DataTableMappingCollection**. Si el nombre proporcionado ya existe, se iniciará una excepción.

## <a name="handle-multiple-result-sets"></a>Control de varios conjuntos de resultados

Cuando **SelectCommand** devuelve varias tablas, **Fill** genera automáticamente nombres de tabla con valores secuenciales para todas las tablas del objeto **DataSet**, comenzando por el nombre de tabla especificado y continuando con el formato **TableName** *N*, a partir de **TableName1**. Puede usar asignaciones de tabla para asignar el nombre generado automáticamente a un nombre que quiera especificar para la tabla en el objeto **DataSet**. Por ejemplo, cuando **SelectCommand** devuelve dos tablas, **Customers** y **Orders**, puede emitir la llamada siguiente a **Fill**.

```csharp
adapter.Fill(customersDataSet, "Customers");
```

Se crean dos tablas en el objeto **DataSet**: **Customers** y **Customers1**. Puede usar asignaciones de tabla para asegurarse de que la segunda se denomina **Orders** en lugar de **Customers1**. Para ello, asigne la tabla de origen de **Customers1** a la tabla **Orders** del objeto **DataSet**, como se muestra en el ejemplo siguiente.

[!code-csharp[SqlDataAdapter_TableMappings#3](~/../sqlclient/doc/samples/SqlDataAdapter_TableMappings.cs#3)]

## <a name="see-also"></a>Consulte también

- [Objetos DataAdapter y DataReader](dataadapters-datareaders.md)
- [Recuperación y modificación de datos en ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET para SQL Server](microsoft-ado-net-sql-server.md)
