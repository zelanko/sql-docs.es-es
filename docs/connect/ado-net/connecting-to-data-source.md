---
title: Conexión al origen de datos
description: Obtenga información sobre los objetos Connection, que se usan para conectarse a orígenes de datos en ADO.NET. El objeto Connection elegido depende del tipo de origen de datos.
ms.date: 11/13/2020
ms.assetid: 9abc3f92-1be3-4e1a-b360-762dc689650e
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: ab6edc2a7090de85e970445cdb2b86d6ed5cb8f2
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126591"
---
# <a name="connecting-to-a-data-source-in-adonet"></a>Conexión a un origen de datos en ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

En el proveedor de datos SqlClient de Microsoft, se utiliza un objeto **Connection** para conectar con un determinado origen de datos mediante una cadena de conexión en la que se proporciona la información de autenticación necesaria. El objeto **Connection** utilizado depende del tipo de origen de datos.

El proveedor de datos SqlClient de Microsoft para SQL Server incluye un tipo <xref:Microsoft.Data.SqlClient.SqlConnection> que se deriva de una clase <xref:System.Data.Common.DbConnection>.

## <a name="in-this-section"></a>En esta sección  

[Establecimiento de la conexión](establishing-connection.md)\
Describe cómo se establece una conexión con un origen de datos mediante un objeto **Connection**.

[Eventos de conexión](connection-events.md)\
Describe la forma de usar un evento **InfoMessage** para recuperar mensajes informativos de un origen de datos.

## <a name="see-also"></a>Vea también

- [Cadenas de conexión](connection-strings.md)
- [Agrupar conexiones](connection-pooling.md)
