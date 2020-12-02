---
title: Recuperación y modificación de datos
description: En .NET Framework, el proveedor de datos SqlClient de Microsoft para SQL Server sirve como puente entre una aplicación y un origen de datos para leer y actualizar datos.
ms.date: 11/13/2020
ms.assetid: 722e7f87-3691-46c6-87e8-7d159722d675
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: cbe61aafd8dcd1681230c355187a65a231535e00
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126575"
---
# <a name="retrieving-and-modifying-data-in-adonet"></a>Recuperación y modificación de datos en ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

La principal función de cualquier aplicación de base de datos es conectarse a un origen de datos y recuperar los datos que contiene. Los proveedores de datos SqlClient sirven como puente entre una aplicación y un origen de datos, permitiéndole ejecutar comandos y recuperar datos mediante un elemento **DataReader** o **DataAdapter**. Una función clave de cualquier aplicación de base de datos es la capacidad de actualizar los datos almacenados en la misma. En el proveedor de datos SqlClient de Microsoft para SQL Server, la actualización de los datos implica el uso de los objetos **DataAdapter**, <xref:System.Data.DataSet> y **Command**; y también puede implicar el uso de transacciones.

## <a name="in-this-section"></a>En esta sección

[Conexión a un origen de datos](connecting-to-data-source.md) Describe cómo establecer una conexión a un origen de datos y cómo trabajar con eventos de conexión.

[Cadenas de conexión](connection-strings.md) Contiene temas que describen varios aspectos del uso de cadenas de conexión, como las palabras clave de la cadena de conexión, la información sobre seguridad y su almacenamiento y recuperación.

[Agrupación de conexiones](connection-pooling.md) Describe la agrupación de conexiones para el proveedor de datos SqlClient de Microsoft para SQL Server.

## <a name="see-also"></a>Vea también

- [Asignaciones de tipos de datos en ADO.NET](data-type-mappings-ado-net.md)
- [SQL Server y ADO.NET](./sql/index.md)
