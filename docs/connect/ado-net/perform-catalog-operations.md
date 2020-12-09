---
title: Realización de operaciones de catálogo
description: Describe la forma de ejecutar comandos que modifican esquemas de la base de datos.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: e60f542f-6271-495b-a9e4-48553481c2a3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 85e68bd77b11fd70e4071d7ae67ebf26c643b540
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428299"
---
# <a name="performing-catalog-operations"></a>Realización de operaciones de catálogo

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Para ejecutar un comando que modifique una base de datos o un catálogo, por ejemplo una instrucción CREATE TABLE o CREATE PROCEDURE, debe crear un objeto **Command** mediante las instrucciones SQL adecuadas y un objeto **Connection**. Ejecute el comando con el método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> del objeto <xref:Microsoft.Data.SqlClient.SqlCommand>.

## <a name="example"></a>Ejemplo

En el ejemplo de código siguiente se crea un procedimiento almacenado en una base de datos de Microsoft SQL Server.

[!code-csharp[DataWorks SqlCommand.ExecuteNonQuery#3](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery_SP_DML.cs#3)]

## <a name="see-also"></a>Vea también

- [Uso de comandos para modificar datos](use-commands-to-modify-data.md)
- [Comandos y parámetros](commands-parameters.md)
