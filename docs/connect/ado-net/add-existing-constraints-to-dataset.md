---
title: Adición de las restricciones existentes a un conjunto de datos
description: Se describe cómo agregar restricciones existentes a un objeto DataSet.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 9471f62c36604cb01ea78f558ac3bfbcb7f4bc01
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772343"
---
# <a name="add-existing-constraints-to-a-dataset"></a>Adición de las restricciones existentes a un conjunto de datos

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

El método <xref:System.Data.Common.DbDataAdapter.Fill%2A> de <xref:Microsoft.Data.SqlClient.SqlDataAdapter> rellena un objeto <xref:System.Data.DataSet> solo con las columnas y filas de un origen de datos. Aunque el origen de datos suele establecer restricciones, el método **Fill** no agrega de forma predeterminada esta información del esquema al objeto **DataSet**.

Para llenar un objeto **DataSet** con la información de restricciones de clave principal existentes de un origen de datos, puede llamar al método <xref:System.Data.Common.DbDataAdapter.FillSchema%2A> de **DataAdapter**, o bien establecer la propiedad <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> de **DataAdapter** en **AddWithKey** antes de llamar a **Fill**. De esta forma se garantiza que las restricciones de clave principal del objeto **DataSet** reflejen las del origen de datos.

> [!NOTE]
> La información de restricciones de clave externa no se incluye y se debe crear de forma explícita.

Al agregar la información del esquema a un objeto **DataSet** antes de rellenarlo con datos, se garantiza que se incluyan las restricciones de clave principal con los objetos <xref:System.Data.DataTable> de **DataSet**. Como resultado, al realizar llamadas adicionales para rellenar el objeto **DataSet**, la información de la columna de clave principal se usa para hacer coincidir las nuevas filas del origen de datos con las filas actuales de cada instancia de **DataTable**, y los datos actuales de las tablas se sobrescriben con los del origen de datos. Sin la información del esquema, las filas nuevas del origen de datos se agregan al objeto **DataSet**, lo que genera filas duplicadas.

> [!NOTE]
> Si una columna del origen de datos es de incremento automático, el método <xref:System.Data.Common.DbDataAdapter.FillSchema%2A>, o bien el método <xref:System.Data.Common.DbDataAdapter.Fill%2A> con el valor **AddWithKey** en la propiedad <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A>, crea un objeto **DataColumn** con una propiedad **AutoIncrement** establecida en `true`. Pero en este caso tendrá que definir manualmente los valores **AutoIncrementStep** y **AutoIncrementSeed**.

> [!NOTE]
> Al usar **FillSchema** o establecer **MissingSchemaAction** en **AddWithKey**, se necesita procesamiento adicional en el origen de datos para determinar la información de la columna de clave principal. Este proceso adicional puede reducir el rendimiento. Si conoce en la fase de diseño la información de la clave principal, es aconsejable especificar de modo explícito la columna o columnas que la forman para mejorar el rendimiento.

En el ejemplo de código siguiente se muestra cómo agregar la información del esquema a un objeto **DataSet** mediante <xref:System.Data.Common.DbDataAdapter.FillSchema%2A>:

[!code-csharp[SqlDataAdapter_FillDataSet#1](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#1)]

En el ejemplo de código siguiente se muestra cómo agregar la información del esquema a un objeto **DataSet** mediante la propiedad <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A> y el método <xref:System.Data.Common.DbDataAdapter.Fill%2A>:

[!code-csharp[SqlDataAdapter_FillDataSet#2](~/../sqlclient/doc/samples/SqlDataAdapter_FillDataSet.cs#2)]

## <a name="handling-multiple-result-sets"></a>Control de varios conjuntos de resultados

Si el objeto **DataAdapter** detecta varios conjuntos de resultados devueltos por <xref:Microsoft.Data.SqlClient.SqlDataAdapter.SelectCommand%2A>, creará varias tablas en el objeto **DataSet**. Las tablas reciben de forma predeterminada un nombre secuencial de base cero **Table** *N*, comenzando por **Table** en lugar de "Table0". Si se pasa un nombre de tabla como argumento al método <xref:System.Data.Common.DbDataAdapter.FillSchema%2A>, las tablas reciben el nombre secuencial en base cero **TableName** *N*, comenzando por **TableName** en lugar de "TableName0".

## <a name="see-also"></a>Consulte también

- [Objetos DataAdapter y DataReader](dataadapters-datareaders.md)
- [Recuperación y modificación de datos en ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET para SQL Server](microsoft-ado-net-sql-server.md)
