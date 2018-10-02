---
title: Configuración de topología (replicación punto a punto) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.p2pwizard.peers.f1
ms.assetid: 5377c59f-2e25-4852-a306-c87ae3dca9fd
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edd8ea9a11a06182dced486ed1b03f1b916e15e4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47793263"
---
# <a name="configure-topology-peer-to-peer-replication"></a>Configurar topología (replicación punto a punto)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice la página **Configurar topología** para realizar las tareas de configuración comunes, como agregar nuevos nodos, eliminando nodos y agregar las nuevas conexiones entre los nodos existentes. El nodo que seleccionó en la página **Publicación** de este asistente se muestra en la superficie de diseño. Para especificar las opciones de configuración, haga clic con el botón secundario en un nodo, una conexión o la superficie de diseño.  
  
> [!NOTE]  
>  El Asistente de configuración de la topología punto a punto solicita información de la topología cuando se cierra el asistente. Si el asistente se cierra y se vuelve a abrir antes de que todos los nodos respondan a la solicitud de información, el asistente puede mostrar una red parcial.  
  
## <a name="options"></a>Opciones  
 La página **Configurar topología** contiene los elementos de interfaz y las opciones que están disponibles al hacer clic con el botón secundario en un elemento. En la tabla siguiente se describe cada elemento de interfaz.  
  
|Elemento de interfaz.|Descripción|  
|-----------------------|-----------------|  
|Superficie de diseño|Muestra otros elementos de interfaz. Para agregar elementos, haga clic con el botón secundario en la superficie de diseño.|  
|![El primer nodo de una topología](../../relational-databases/replication/media/p2pwizard-firstnode.gif "El primer nodo de una topología")|El nodo original en la topología. Los nodos nuevos se inicializan utilizando una copia de la base de datos de publicación del nodo original.|  
|![Un nodo para el que tenemos información completa](../../relational-databases/replication/media/p2pwizard-complete.gif "Un nodo para el que tenemos información completa")|Un nodo que está ejecutando una instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o una versión posterior, para el que la replicación tiene información completa. Para especificar las opciones de configuración, haga clic con el botón secundario en el nodo.|  
|![Un nodo para el que tenemos información incompleta](../../relational-databases/replication/media/p2pwizard-incomplete.gif "Un nodo para el que tenemos información incompleta")|Un nodo para el que la replicación tiene información incompleta. Para especificar las opciones de configuración, haga clic con el botón secundario en el nodo.<br /><br /> La replicación tiene información incompleta debido a una de las razones siguientes:<br /><br /> -El nodo está ejecutando una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], que no almacena todos los metadatos requeridos por el asistente.<br /><br /> -El nodo está ejecutando una versión posterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero la replicación no puede recuperar información de la suscripción del nodo. Para solucionar esta situación:<br /><br /> Asegúrese de que la base de datos en el nodo está en línea y que puede conectar con ella utilizando las mismas credenciales que los Agentes de distribución que se conectan al nodo.<br /><br /> Asegúrese de que se estén ejecutando el Agente del registro del LOG y los Agentes de distribución que se conectan al nodo.<br /><br /> Asegúrese de que el tiempo de espera de actualización esté establecido en un valor suficientemente alto para recopilar toda la información de la topología. Para establecer el tiempo de espera, haga clic con el botón secundario en la superficie de diseño y haga clic en **Establecer tiempo de espera de la actualización**.|  
|Línea gris con flechas|La conexión entre dos nodos. Para agregar una conexión, haga clic con el botón secundario en uno de los nodos que desea conectar. Para quitar una conexión, haga clic con el botón secundario en la conexión.<br /><br /> Si la línea tiene una flecha única, la replicación tiene información incompleta para uno de los nodos.|  
  
### <a name="options-for-the-design-surface"></a>Opciones para la superficie de diseño  
 **Volver a dibujar el gráfico**  
 Actualiza los objetos en la superficie de diseño sin actualizar la topología. Al actualizar, se podría proporcionar una mejor vista de la topología.  
  
 **Actualizar la topología**  
 Consulta cada nodo en la topología y muestra la información actualizada sobre cada nodo. Con muchos nodos, este proceso puede tardar varios minutos.  
  
 Si el asistente solicita información de la topología y a continuación se cierra y se vuelve a abrir antes de que todos los nodos respondan a la solicitud, esta página podría no mostrar todos los nodos en la topología.  
  
 **Agregar un nuevo nodo del mismo nivel**  
 Agrega una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la topología punto a punto. Agregar una instancia como nodo crea una publicación en esa instancia después de que el asistente se complete. Tras agregar el nodo, haga clic con el botón secundario en él para agregar una conexión entre el nuevo nodo y un nodo existente.  
  
 Para participar en una topología punto a punto, la instancia debe cumplir los requisitos siguientes:  
  
-   Debe estar configurada como Distribuidor o estar asociada con un Distribuidor remoto.  
  
-   Debe contener una copia de la base de datos implicada en replicación. Esta copia es normalmente una copia de seguridad restaurada de la base de datos de publicación original.  
  
 **Seleccionar nodos para verlos**  
 Selecciona qué nodos desea ver en la superficie de diseño. Esta opción es útil si la topología tiene un gran número de nodos. Sea consciente de que solamente puede agregar conexiones entre nodos que están visibles en la superficie de diseño.  
  
 **Establecer tiempo de espera de la actualización**  
 Especifica cuánto tiempo se puede ejecutar el proceso de la actualización antes de que se supere el tiempo de espera de la operación.  
  
### <a name="options-for-each-node"></a>Opciones para cada nodo  
 **Agregar una nueva conexión del mismo nivel**  
 Agrega una conexión entre dos nodos. Por ejemplo, si agrega una conexión entre el Nodo A y el Nodo B, la replicación agrega dos suscripciones: la primera habilita el Nodo A para recibir los cambios de la publicación en el Nodo B y la segunda permite al Nodo B recibir cambios de la publicación en el Nodo A.  
  
 **Eliminar nodo del mismo nivel**  
 Quita un nodo de la topología. Por ejemplo, si quita el Nodo C, se quita la publicación en ese nodo. También se quitan las suscripciones entre el Nodo A y el Nodo C, y el Nodo B y el Nodo C. No se elimina la base de datos del Nodo C y no se deshabilitan la publicación y la distribución.  
  
> [!NOTE]  
>  Al configurar la replicación punto a punto, se especifica un identificador para cada nodo. Este identificador, que debe ser único en todos los nodos de la topología, se almacena en la columna originator_id de la tabla del sistema [MSpeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md). Si un nodo se quita de la topología, el identificador se sigue conservando en la tabla de historial. El identificador se conserva para evitar que se produzcan falsos conflictos si hay cambios procedentes del nodo quitado que todavía se están replicando en la topología. Si desea volver a usar el identificador para un nuevo nodo, primero deberá eliminarlo manualmente de la tabla MSpeer_originatorid_history en todos los nodos. Antes de eliminar un identificador de un nodo, ejecute [sp_requestpeerresponse](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) para comprobar que todos los cambios que se originaron desde ese nodo se han replicado.  
  
 **Conectar a todos los nodos mostrados**  
 Agrega conexiones entre el nodo seleccionado y todos los otros nodos. Por ejemplo, si ha seleccionado esta opción para el Nodo C en una topología de tres nodos, la replicación agrega cuatro suscripciones: dos que habilitan el Nodo A y el Nodo B para recibir los cambios de la publicación en el Nodo C y dos que permiten que el Nodo C reciba cambios de las publicaciones en el Nodo A y el Nodo B.  
  
 **Seleccionar nodos para verlos**  
 Selecciona qué nodos desea ver en la superficie de diseño. Esta opción es útil si la topología tiene un gran número de nodos. Sea consciente de que solamente puede agregar conexiones entre nodos que están visibles en la superficie de diseño.  
  
### <a name="options-for-the-connection-arrows"></a>Opciones de las flechas de conexión  
 **Quitar conexión del mismo nivel**  
 Quita una conexión entre dos nodos. Por ejemplo, si quita una conexión entre el Nodo A y el Nodo B, la replicación elimina dos suscripciones: la que habilita el Nodo A para recibir los cambios de la publicación en el Nodo B y la que permite al Nodo B recibir cambios de la publicación en el Nodo A.  
  
## <a name="see-also"></a>Ver también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Administrar una topología punto a punto &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)  
  
  
