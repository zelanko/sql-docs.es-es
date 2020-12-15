---
title: Paginación de resultados de consulta
description: Proporciona un ejemplo de cómo ver los resultados de una consulta como páginas de datos.
ms.date: 11/30/2020
dev_langs:
- csharp
ms.assetid: fa360c46-e5f8-411e-a711-46997771133d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 2de305e1069964f2d1a67b7f201578c7448d3e09
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2020
ms.locfileid: "96772282"
---
# <a name="paging-through-a-query-result"></a>Paginación de resultados de consulta

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

La paginación a través del resultado de una consulta es un proceso que consiste en devolver los resultados de una consulta en subconjuntos menores de datos, o páginas. Se trata de una práctica frecuente para presentar los resultados a un usuario en fragmentos pequeños y fáciles de administrar.

<xref:Microsoft.Data.SqlClient.SqlDataAdapter> permite devolver únicamente una página de datos mediante sobrecargas del método <xref:System.Data.Common.DbDataAdapter.Fill%2A>. Pero es posible que no sea la mejor opción para realizar la paginación por medio de resultados de consultas grandes, ya que, aunque el objeto **DataAdapter** rellena los elementos <xref:System.Data.DataTable> o <xref:System.Data.DataSet> de destino solo con los registros solicitados, se siguen utilizando los recursos para devolver toda la consulta.

Para devolver una página de datos a partir de un origen de datos sin utilizar los recursos necesarios para devolver toda la consulta, hay que especificar otros criterios adicionales para la consulta que reduzcan las filas devueltas a las filas únicamente necesarias.

Para usar el método <xref:System.Data.Common.DbDataAdapter.Fill%2A> a fin de devolver una página de datos, especifique un parámetro **startRecord** que represente el primer registro de la página de datos, y un parámetro **maxRecords** que represente el número de registros de la página de datos.

## <a name="example"></a>Ejemplo

En el ejemplo de código siguiente se muestra cómo usar el método <xref:System.Data.Common.DbDataAdapter.Fill%2A> para devolver la primera página del resultado de una consulta cuando el tamaño de la página es de cinco registros.

[!code-csharp[SqlDataAdapter_Paging#1](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#1)]

En el ejemplo anterior, el objeto **DataSet** solo se rellena con cinco registros pero se devuelve la tabla **Orders** completa. Para rellenar el objeto **DataSet** con esos mismos cinco registros, pero devolver únicamente cinco registros, use las cláusulas `TOP` y `WHERE` en la instrucción SQL, como en el ejemplo de código siguiente.

[!code-csharp[SqlDataAdapter_Paging#2](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#2)]

> [!NOTE]
> Al realizar la paginación por los resultados de la consulta de esta manera, debe conservar el elemento `unique identifier` que ordena las filas, a fin de pasar el identificador único al comando para devolver la siguiente página de registros, como se muestra en el ejemplo de código siguiente.

[!code-csharp[SqlDataAdapter_Paging#4](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#4)]

Para devolver el valor `next page of records` mediante la sobrecarga del método **Fill** que toma los parámetros **startRecord** y **maxRecords**, incremente el índice del registro actual por el tamaño de página y rellene la tabla.

> [!NOTE]
> Recuerde que el servidor de bases de datos devuelve todos los resultados de la consulta aunque solo se agregue una página de registros al objeto **DataSet**.

En el siguiente ejemplo de código se vacía el contenido de las filas de la tabla antes de rellenarse con la siguiente página de datos. Quizás se desee conservar un cierto número de filas devueltas en una caché local para reducir los viajes al servidor de bases de datos.

[!code-csharp[SqlDataAdapter_Paging#3](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#3)]

Para devolver la siguiente página de registros sin que el servidor de bases de datos tenga que devolver toda la consulta, hay que especificar criterios restrictivos en la instrucción SELECT. Como el ejemplo anterior conservaba el último registro devuelto, es posible utilizarlo en la cláusula WHERE con el fin de especificar un punto de partida para la consulta, como se muestra en el ejemplo de código siguiente.

[!code-csharp[SqlDataAdapter_Paging#5](~/../sqlclient/doc/samples/SqlDataAdapter_Paging.cs#5)]

## <a name="see-also"></a>Consulte también

- [Objetos DataAdapter y DataReader](dataadapters-datareaders.md)
- [Microsoft ADO.NET para SQL Server](microsoft-ado-net-sql-server.md)
