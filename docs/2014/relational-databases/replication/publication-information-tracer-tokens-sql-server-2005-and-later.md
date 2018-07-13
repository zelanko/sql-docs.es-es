---
title: Información de publicación, testigos de seguimiento (publicación transaccional, SQL Server 2005 y versiones posterior) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.publicationinfo.tracertokens.f1
ms.assetid: a115ba95-17ae-45df-91bd-5a1a35f3745f
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ea4849d69bc1552141709180f00d38f1efb72549
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37278921"
---
# <a name="publication-information-tracer-tokens-transactional-publication-sql-server-2005-and-later"></a>Información de la publicación, Testigos de seguimiento (Publicación transaccional, SQL Server 2005 y posterior)
  La pestaña **Testigos de seguimiento** le permitirá validar las conexiones y medir la latencia de un sistema que utiliza la replicación transaccional. Se escribe un token (una pequeña cantidad de datos) en el registro de transacción de la base de datos de publicaciones, marcado como si fuese una transacción replicada, y se envía a través del sistema, de forma que permite calcular:  
  
-   Cuánto tiempo transcurre desde que se confirma una transacción en el publicador hasta que se inserta el comando correspondiente en la base de datos de distribución del distribuidor.  
  
-   Cuánto tiempo transcurre desde que se inserta un comando en la base de datos de distribución hasta que se confirma la transacción correspondiente en el suscriptor.  
  
 A partir de estos cálculos, podrá responder a diversas preguntas, como por ejemplo:  
  
-   ¿Qué suscriptores tardan más en recibir un cambio del publicador?  
  
-   De los suscriptores que esperan recibir el testigo de seguimiento, ¿cuáles, si los hay, no lo han recibido?  
  
## <a name="options"></a>Opciones  
 Para cambiar la manera que la cuadrícula muestra los datos, haga clic con el botón secundario en la cuadrícula y, a continuación, haga clic en una de las opciones siguientes:  
  
-   **Ordenar**: ordene en una o más columnas en el cuadro de diálogo **Ordenar columnas** .  
  
-   **Elegir columnas para mostrar**: seleccione las columnas que se mostrarán y el orden en el que se mostrarán en el cuadro de diálogo **Elegir columnas** .  
  
-   **Filtro**: filtre filas en la cuadrícula basándose en los valores de columna en el cuadro de diálogo **Configuración del filtro** .  
  
-   **Borrar filtro**: borre cualquier configuración de filtro para la cuadrícula.  
  
 La configuración del filtro es específica de cada cuadrícula. La selección y ordenación de las columnas se aplica a todas las cuadrículas del mismo tipo, como la cuadrícula de las publicaciones para cada Publicador.  
  
 **Insertar seguimiento**  
 Haga clic para insertar un testigo de seguimiento en el registro de transacciones del publicador.  
  
 **Hora de inserción**  
 Seleccione la hora de inserción del testigo de seguimiento para mostrar la información de latencia a partir de ese momento. De forma predeterminada, se mostrará la información a partir de la hora más reciente.  
  
> [!NOTE]  
>  La información del testigo de seguimiento se guarda durante el mismo período que otros datos del historial, que depende del período de retención de historial de la base de datos de distribución. Para obtener información sobre cómo cambiar las propiedades de la base de datos de distribución, vea [Ver y modificar las propiedades del distribuidor y del publicador](view-and-modify-distributor-and-publisher-properties.md).  
  
 **Suscripción**  
 Nombre de cada suscripción a la publicación.  
  
 **Publicador a distribuidor**  
 Tiempo que transcurre desde que se confirma una transacción en el publicador hasta que se inserta el comando correspondiente en la base de datos de distribución del distribuidor. Si un valor muestra **Pendiente** indica que el token aún no ha llegado al distribuidor. Si persiste el estado pendiente, compruebe que se esté ejecutando el Agente de registro del LOG.  
  
 **Distribuidor a suscriptor**  
 Tiempo que transcurre desde que se inserta un comando en la base de datos de distribución hasta que se confirma la transacción correspondiente en el suscriptor. Si un valor muestra **Pendiente** indica que el token aún no ha llegado al suscriptor. Si persiste el estado pendiente, compruebe que se esté ejecutando el Agente de distribución.  
  
 **Latencia total**  
 Tiempo que transcurre desde que se confirma una transacción en el publicador hasta que se confirma la transacción correspondiente en el suscriptor. Representa la latencia de un extremo a otro del sistema de replicación del suscriptor en dicho momento. Si un valor muestra **Pendiente** indica que el token aún no ha llegado al suscriptor.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Iniciar el Monitor de replicación](monitor/start-the-replication-monitor.md)   
 [Medir la latencia y validar las conexiones de la replicación transaccional](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)   
 [Supervisar el rendimiento con el Monitor de replicación](monitor/monitor-performance-with-replication-monitor.md)   
 [Monitoring Replication](monitoring-replication.md)  (Supervisar la replicación)  
 [Información general sobre los agentes de replicación](agents/replication-agents-overview.md)  
  
  
