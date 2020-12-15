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
ms.openlocfilehash: d6e4d6c298c632c446e1671b5d9adabaa19e0776
ms.sourcegitcommit: c127c0752e84cccd38a7e23ac74c0362a40f952e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/07/2020
ms.locfileid: "96761493"
---
# <a name="retrieving-and-modifying-data-in-adonet"></a>Recuperación y modificación de datos en ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

La principal función de cualquier aplicación de base de datos es conectarse a un origen de datos y recuperar los datos que contiene. Los proveedores de datos SqlClient sirven como puente entre una aplicación y un origen de datos, permitiéndole ejecutar comandos y recuperar datos mediante un elemento **DataReader** o **DataAdapter**. Una función clave de cualquier aplicación de base de datos es la capacidad de actualizar los datos almacenados en la misma. En el proveedor de datos SqlClient de Microsoft para SQL Server, la actualización de los datos implica el uso de los objetos **DataAdapter**, <xref:System.Data.DataSet> y **Command**; y también puede implicar el uso de transacciones.

## <a name="in-this-section"></a>En esta sección

[Conexión a un origen de datos](connecting-to-data-source.md)  
Describe cómo se establece una conexión con un origen de datos y cómo trabajar con eventos de conexión.

[Cadenas de conexión](connection-strings.md)  
Contiene temas en los que se describen varios aspectos del uso de cadenas de conexión, entre los que se incluyen las palabras clave de cadena de conexión, información sobre seguridad y el almacenamiento y recuperación de cadenas de conexión.

[Agrupación de conexiones](connection-pooling.md)  
Se describe la agrupación de conexiones para el proveedor de datos SqlClient de Microsoft para SQL Server.

[Comandos y parámetros](commands-parameters.md)  
Contiene temas en los que se describe cómo crear comandos y generadores de comandos, configurar parámetros y cómo ejecutar comandos para recuperar y modificar datos.

[Objetos DataAdapter y DataReader](dataadapters-datareaders.md)  
Contiene temas en los que se describen DataReaders, DataAdapters, los parámetros, el control de eventos DataAdapter y la ejecución de operaciones por lotes.

## <a name="see-also"></a>Vea también

- [Asignaciones de tipos de datos en ADO.NET](data-type-mappings-ado-net.md)
- [SQL Server y ADO.NET](./sql/index.md)
- [Microsoft ADO.NET para SQL Server](microsoft-ado-net-sql-server.md)
