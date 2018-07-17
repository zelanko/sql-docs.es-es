---
title: incluir archivo
description: incluir archivo
services: sql-database
author: MightyPen
ms.service: sql-database
ms.topic: include
ms.date: 04/05/2018
ms.author: genemi
ms.custom: include file
ms.openlocfilehash: 842a7377bcd6bdcb649a78b2f31eb66de95bc5a3
ms.sourcegitcommit: 44e9bf62f2c75449c17753ed66bf85c43928dbd5
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854397"
---
## <a name="specifying-application-intent"></a>Especificar el intento de la aplicación

La palabra clave **ApplicationIntent** puede especificarse en la cadena de conexión. Los valores asignables son **ReadWrite** o **ReadOnly**. El valor predeterminado es **ReadWrite**.

Cuando **ApplicationIntent = ReadOnly**, el cliente solicita una carga de trabajo de lectura al conectarse. El servidor aplica la intención en tiempo de conexión y durante un **USE** instrucción de base de datos.

La palabra clave **ApplicationIntent** no funciona con bases de datos de solo lectura heredadas.  


#### <a name="targets-of-readonly"></a>Destinos de solo lectura

Cuando se elige una conexión **ReadOnly**, la conexión se asigna a cualquiera de las siguientes configuraciones especiales que podrían existir la base de datos:

- [Always On](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - Una base de datos puede permitir o denegar la lectura de las cargas de trabajo en la base de datos de destino Always On. Esta opción se controla mediante el **ALLOW_CONNECTIONS** cláusula de la **PRIMARY_ROLE** y **SECONDARY_ROLE** instrucciones Transact-SQL.

- [Replicación geográfica](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [Escalado horizontal de lectura](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

Si ninguno de esos destinos especiales están disponible, es de lectura de la base de datos normal.

&nbsp;

El **ApplicationIntent** permite la palabra clave *enrutamiento de solo lectura*.


## <a name="read-only-routing"></a>Enrutamiento de solo lectura

El enrutamiento de solo lectura es una característica que puede asegurar la disponibilidad de una réplica de solo lectura de una base de datos. Para habilitar el enrutamiento de solo lectura, se aplican todas las opciones siguientes:

- Debe conectarse siempre a un agente de escucha de grupo de disponibilidad Always On.

- La palabra clave de cadena de conexión de **ApplicationIntent** debe establecerse en **ReadOnly**.

- El administrador de bases de datos debe configurar el grupo de disponibilidad para habilitar el enrutamiento de solo lectura.

Varias conexiones con el enrutamiento de solo lectura no todos se conecten a la misma réplica de solo lectura. Los cambios en la sincronización de la base de datos o los cambios en la configuración de enrutamiento del servidor pueden producir conexiones de cliente para réplicas de solo lectura diferentes. Puede asegurarse de que todas las solicitudes de solo lectura se conectan a la misma réplica de solo lectura. Garantizar esta similitud por *no* pasando un agente de escucha del grupo de disponibilidad para el **Server** palabra clave de cadena de conexión. En su lugar, especifique el nombre de la instancia de solo lectura.

Enrutamiento de solo lectura puede tardar más que la conexión a la réplica principal. La espera más larga se debe a que el enrutamiento de solo lectura se conecta primero a la principal y, luego, busca la mejor instancia secundaria legible que esté disponible. Debido a estos staps varios, debe aumentar el tiempo de espera de inicio de sesión para al menos 30 segundos.

