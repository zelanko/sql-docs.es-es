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
ms.sourcegitcommit: a98ed7872afc055c65aa9697d571f8b300f6eeb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313401"
---
## <a name="specifying-application-intent"></a>Especificar el intento de la aplicación

La palabra clave **ApplicationIntent** puede especificarse en la cadena de conexión. Los valores asignables son **ReadWrite** o **ReadOnly**. El valor predeterminado es **ReadWrite**.

Cuando **ApplicationIntent = ReadOnly**, el cliente solicita una carga de trabajo de lectura al conectarse. El servidor aplicará la intención en el momento de la conexión y durante un **USE** instrucción de base de datos.

El **ApplicationIntent** palabra clave no funciona con bases de datos heredadas de solo lectura.  


#### <a name="targets-of-readonly"></a>Destinos de solo lectura

Cuando se elige una conexión **ReadOnly**, la conexión se asigna a cualquiera de las siguientes configuraciones especiales que podrían existir la base de datos:

- [AlwaysOn](~/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)
    - Una base de datos puede permitir o denegar cargas de trabajo de lectura en la base de datos de inicio de siempre en destino. Esta opción se controla mediante la **ALLOW_CONNECTIONS** cláusula de la **PRIMARY_ROLE** y **SECONDARY_ROLE** instrucciones Transact-SQL.

- [Replicación geográfica](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview)

- [Leer de escalabilidad horizontal](https://docs.microsoft.com/azure/sql-database/sql-database-read-scale-out)

Si ninguno de esos objetivos especiales están disponible, es de lectura de la base de datos normal.

&nbsp;

El **ApplicationIntent** palabra clave permite *enrutamiento de solo lectura*.


## <a name="read-only-routing"></a>Enrutamiento de solo lectura

El enrutamiento de solo lectura es una característica que puede asegurar la disponibilidad de una réplica de solo lectura de una base de datos. Para habilitar el enrutamiento de solo lectura, se aplican todas las opciones siguientes:

- Debe conectarse siempre a un agente de escucha de grupo de disponibilidad Always On.

- La palabra clave de cadena de conexión de **ApplicationIntent** debe establecerse en **ReadOnly**.

- El administrador de bases de datos debe configurar el grupo de disponibilidad para habilitar el enrutamiento de solo lectura.

Varias conexiones con el enrutamiento de solo lectura no todas se conecten a la misma réplica de solo lectura. Los cambios en la sincronización de la base de datos o los cambios en la configuración de enrutamiento del servidor pueden producir conexiones de cliente para réplicas de solo lectura diferentes. Puede asegurarse de que todas las solicitudes de solo lectura se conectan a la misma réplica de solo lectura. Asegúrese de esta similitud por *no* pasando un agente de escucha del grupo de disponibilidad para el **Server** palabra clave de cadena de conexión. En su lugar, especifique el nombre de la instancia de solo lectura.

Enrutamiento de solo lectura puede tardar más que la conexión a la réplica principal. La espera más tiempo porque el enrutamiento de solo lectura en primer lugar se conecta a la réplica principal y, a continuación, busca el mejor secundario legible disponible. Debido a estos staps varios, debe aumentar el tiempo de espera de inicio de sesión para que al menos 30 segundos.

