---
title: Agrupación de conexiones
description: Obtenga información sobre la agrupación de conexiones, una técnica de optimización que ADO.NET usa para minimizar el costo de abrir conexiones a orígenes de datos.
ms.date: 11/13/2020
ms.assetid: 955c057f-aea8-4ba8-aa6d-e3dfa18ba8d5
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 41842a2eb754aedc31bad206ad427a86bb65f00f
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/25/2020
ms.locfileid: "96126587"
---
# <a name="connection-pooling"></a>Agrupación de conexiones

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

La conexión a un origen de datos puede ser un proceso largo. Para reducir el costo de abrir conexiones, ADO.NET emplea una técnica de optimización llamada *agrupación de conexiones*, que reduce el costo de abrir y cerrar conexiones repetidas veces.

## <a name="in-this-section"></a>En esta sección  

[Agrupación de conexiones de SQL Server (ADO.NET)](sql-server-connection-pooling.md) Proporciona información general sobre la agrupación de conexiones y describe cómo funciona la agrupación de conexiones en SQL Server.

## <a name="see-also"></a>Vea también

- [Recuperar y modificar datos en ADO.NET](retrieving-modifying-data.md)
