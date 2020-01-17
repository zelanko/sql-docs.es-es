---
title: Detección avanzada y solución de conflictos (combinación)
description: Obtenga información sobre métodos de detección y resolución de conflictos con la replicación.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- column-level conflict tracking
- row-level conflict tracking
- viewing merge replication conflicts
- resolving merge replication conflicts
- logical record-level conflict tracking [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 063d3d9c-ccb5-4fab-9d0c-c675997428b4
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f90625c1aa123cf72b93ce815b02cccd7cedc78a
ms.sourcegitcommit: 02d44167a1ee025ba925a6fefadeea966912954c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2019
ms.locfileid: "75321612"
---
# <a name="advanced-merge-replication---conflict-detection-and-resolution"></a>Replicación de mezcla avanzada: detección y resolución de conflictos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Cuando un publicador y un suscriptor se conectan y se produce la sincronización, el Agente de mezcla detecta si existen conflictos. Si se detectan conflictos, el Agente de mezcla utiliza un solucionador de conflictos (que se especifica cuando se agrega un artículo a una publicación) para determinar qué datos se aceptarán y se propagarán a otros sitios.  

 La replicación de mezcla ofrece diversos métodos para detectar y solucionar conflictos. Para la mayoría de aplicaciones, el método predeterminado es el adecuado:  
  
-   Si se produce un conflicto entre un publicador y un suscriptor, el cambio del publicador se mantiene y el cambio en el suscriptor se descarta.   
-   Si se produce un conflicto entre dos suscriptores que utilizan suscripciones de cliente (el tipo predeterminado para las suscripciones de extracción), se mantiene el cambio del primer suscriptor que se sincronice con el publicador y se descarta el cambio del segundo suscriptor. Para obtener información sobre cómo especificar las suscripciones de cliente y servidor, consulte [Especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md).   
-   Si se produce un conflicto entre dos suscriptores que utilizan suscripciones de servidor (el tipo predeterminado para las suscripciones de inserción), se mantiene el cambio del suscriptor con el valor de prioridad más alto y se descarta el cambio del segundo suscriptor. Si los valores de prioridad son iguales, se mantiene el cambio del primer suscriptor que se sincronice con el publicador.  
  
> [!NOTE]  
>  Aunque un suscriptor se sincronice con el publicador, suelen producirse conflictos entre las actualizaciones que se realizan en suscriptores diferentes, en vez de entre las actualizaciones que se realizan en un suscriptor y en el publicador.  
  
 El comportamiento de la detección y resolución de conflictos depende de las siguientes opciones, que se describen en este tema:    
-   Si especifica seguimiento por columna, seguimiento por filas o seguimiento por registro lógico.    
-   Si especifica el mecanismo de resolución basado en la prioridad predeterminada o especifica un solucionador de artículos. Un solucionador de artículos puede ser:  
  
    -   Un *controlador de lógica de negocios* escrito en código administrado   
    -   Un *solucionador personalizado*basado en COM    
    -   Un solucionador basado en COM proporcionado por [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
  
     Si se utiliza el mecanismo de resolución predeterminado, el tipo de suscripción utilizada (cliente o servidor) determina el comportamiento.  
  
## <a name="conflict-detection"></a>Detección de conflictos  
 Si un cambio de datos se califica como un conflicto o no depende del tipo de seguimiento de conflictos que ha especificado para un artículo:  
  
-   Si selecciona seguimiento de conflictos por columna, se considera un conflicto si los cambios se realizan en la misma columna de la misma fila en más de un nodo de replicación.    
-   Si selecciona seguimiento de conflictos por filas, se considera un conflicto si los cambios se realizan en cualquier columna de la misma fila en más de un nodo de replicación (las columnas afectadas en las filas correspondientes no tienen que ser las mismas).    
-   Si selecciona seguimiento de conflictos por registro lógico, se considera un conflicto si los cambios se realizan en cualquier fila del mismo registro lógico en más de un nodo de replicación (las columnas afectadas en las filas correspondientes no tienen que ser las mismas).  
  
 Para más información, consulte [Detectar y solucionar conflictos en registros lógicos](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
 Para especificar el nivel de seguimiento y resolución de conflictos de un artículo, consulte [Specify merge replication properties](../../../relational-databases/replication/merge/specify-merge-replication-properties.md) (Especificación de las propiedades de replicación de mezcla).  
  
## <a name="conflict-resolution"></a>Resolución de conflictos  
 Una vez detectado un conflicto, el Agente de mezcla inicia el solucionador de conflictos seleccionado y lo utiliza para determinar el ganador. La fila ganadora se aplica en el publicador y en el suscriptor, y los datos de la fila perdedora se escriben en una tabla de conflictos. Los conflictos se resuelven inmediatamente después de ejecutarse el solucionador, a menos que seleccione solucionar los conflictos de forma interactiva.  

Resolución de conflictos de replicación de mezcla  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]  
  Cuando un publicador y un suscriptor se conectan y se produce la sincronización, el Agente de mezcla detecta si existen conflictos. Si se detectan conflictos, el Agente de mezcla utiliza un solucionador de conflictos para determinar qué datos se aceptarán y se propagarán a otros sitios.  
  
> [!NOTE]  
>  Aunque un suscriptor se sincronice con el publicador, suelen producirse conflictos entre las actualizaciones que se realizan en suscriptores diferentes, en vez de entre las actualizaciones que se realizan entre un suscriptor y el publicador.  
  
 La replicación de mezcla ofrece diversos métodos para detectar y solucionar conflictos. Para la mayoría de aplicaciones, el método predeterminado es el adecuado:  
  
-   Si se produce un conflicto entre un publicador y un suscriptor, el cambio del publicador se mantiene y el cambio en el suscriptor se descarta.  
  
-   Si se produce un conflicto entre dos suscriptores que utilizan suscripciones de cliente (el tipo predeterminado para las suscripciones de extracción), se mantiene el cambio del primer suscriptor que se sincronice con el publicador y se descarta el cambio del segundo suscriptor. Para obtener información sobre cómo especificar las suscripciones de cliente y servidor, consulte [Especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
-   Si se produce un conflicto entre dos suscriptores que utilizan suscripciones de servidor (el tipo predeterminado para las suscripciones de inserción), se mantiene el cambio del suscriptor con el valor de prioridad más alto y se descarta el cambio del segundo suscriptor. Si los valores de prioridad son iguales, se mantiene el cambio del primer suscriptor que se sincronice con el publicador.  
  
 Para obtener más información acerca de cómo detectar y solucionar conflictos en la replicación de mezcla, vea [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### <a name="resolver-types"></a>Tipos de solucionador  
 En la replicación de mezcla, la resolución de conflictos tiene lugar en el nivel de artículo. En el caso de publicaciones compuestas de varios artículos, es posible tener varios solucionadores de conflictos que proporcionen servicio a diferentes artículos o un mismo solucionador de conflictos que proporcione servicio a un artículo, a varios artículos o a todos los artículos que componen la publicación.  
  
 Si va a utilizar el solucionador de conflictos basado en prioridad predeterminado, no tendrá que establecer la propiedad de solucionador de los artículos. Si desea utilizar un solucionador de artículos en lugar del solucionador predeterminado, deberá establecer la propiedad de solucionador del artículo que lo utilizará seleccionando un solucionador personalizado disponible en el publicador. Cualquier información específica que se deba pasar al solucionador puede especificarse también en la propiedad de información de solucionador.  
  
 La replicación de mezcla ofrece cuatro tipos de solucionadores de conflictos:  
  
-   El solucionador de conflictos predeterminado basado en prioridad  
  
     El mecanismo de resolución predeterminada se comporta de forma diferente, dependiendo de si se trata de una suscripción de cliente o una suscripción de servidor. Asigne valores de prioridad a suscriptores individuales que utilizan suscripciones de servidor; los cambios realizados en el nodo con la máxima prioridad ganan en cualquier conflicto. En suscripciones de cliente, el primer cambio escrito en el publicador gana el conflicto.  
  
     Después de crear una suscripción, no se puede cambiar de un tipo a otro.  
  
-   Un controlador de lógica de negocios  
  
     El marco de trabajo de controladores de lógica de negocios permite escribir un ensamblado de código administrado al que se llama durante el proceso de sincronización de mezcla. El ensamblado incluye la lógica de negocios que puede responder a conflictos y a otras condiciones durante la sincronización. Para obtener más información, consulte [Ejecutar lógica de negocios durante la sincronización de mezcla](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
-   Un solucionador personalizado basado en COM  
  
     La replicación de combinación proporciona una API para escribir solucionadores como objetos COM en lenguajes como [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]. Para más información, consulte [COM-Based Custom Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md).  
  
-   Un solucionador basado en COM proporcionado por [!INCLUDE[msCoName](../../../includes/msconame-md.md)]  
  
     [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluye varios solucionadores basados en COM. Para obtener más información, consulte [Solucionadores basados en Microsoft COM](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).  
  
 Para obtener información sobre cómo seleccionar el tipo de solucionador adecuado, consulte [Elegir un solucionador](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-choose-a-resolver.md).  
  
> [!NOTE]  
>  Algunos solucionadores de artículos están escritos para controlar conflictos solo en determinadas operaciones. Por ejemplo, una resolución puede controlar actualizaciones, pero no inserciones o eliminaciones. El solucionador de conflictos predeterminado basado en prioridad controla los conflictos que no controla el solucionador de artículos.  
  
 Para especificar un tipo de suscripción de mezcla y la prioridad de resolución de conflictos, vea  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Especificación de un tipo de suscripción de mezcla y la prioridad de resolución de conflictos &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md)  
  
-   Programación de replicación de [!INCLUDE[tsql](../../../includes/tsql-md.md)] y programación con Replication Management Objects (RMO): [Creación de una suscripción de extracción](../../../relational-databases/replication/create-a-pull-subscription.md) y [Creación de una suscripción de inserción](../../../relational-databases/replication/create-a-push-subscription.md)  
  
### <a name="interactive-resolver"></a>Solucionador interactivo  
 La replicación proporciona una interfaz de usuario Solucionador interactivo que se puede utilizar junto con el solucionador de conflictos basado en prioridad predeterminado o un solucionador de artículos. Cuando se ejecuta una sincronización a petición a través del Administrador de sincronización de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows, el Solucionador interactivo muestra los datos en conflicto en tiempo de ejecución y permite elegir la forma de solucionar los conflictos. Para obtener más información acerca de cómo habilitar la resolución interactiva e iniciar el Solucionador interactivo, vea [Interactive Conflict Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
## <a name="viewing-conflicts"></a>Ver conflictos  
 La forma más directa de ver los conflictos consiste en usar el Visor de conflictos de replicación, disponible en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] también proporciona procedimientos almacenados que permiten consultar tablas de conflictos). El Visor de conflictos y el Solucionador interactivo son herramientas parecidas, pero el Solucionador interactivo permite solucionar los conflictos cuando se realiza la sincronización, mientras que el Visor de conflictos está diseñado para ver los conflictos después de haberlos resuelto. Si los metadatos en conflicto aún están disponibles en las tablas del sistema (los metadatos en conflicto se conservan, de forma predeterminada, durante 14 días), puede reemplazar el resultado de la resolución de conflictos en el Visor de conflictos, pero si se requiere con frecuencia una intervención directa, debe considerar la posibilidad de utilizar el Solucionador interactivo.  
  
> [!NOTE]  
>  Los conflictos que implican registros lógicos no se muestran en el Visor de conflictos. Para ver información acerca de estos conflictos, utilice procedimientos almacenados de replicación. Para obtener más información, vea [Ver información de conflictos para publicaciones de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md).  
  
 El Visor de conflictos muestra información de tres tablas del sistema:  
  
-   La replicación crea una tabla de conflictos por cada tabla de un artículo de mezcla, con un nombre en formato **MSmerge_conflict_\<NombreDePublicación>_\<NombreDeArtículo>** .  
  
     Las tablas de conflictos tienen la misma estructura que las tablas en las que se basan. Una fila de una de estas tablas consta de la versión perdedora de una fila de conflictos (la versión ganadora de esta fila se encuentra en la tabla real del usuario).  
  
-   En la tabla **MSmerge_conflicts_info** se proporciona información sobre cada conflicto, incluido el tipo de conflicto.  
  
-   En la tabla **sysmergearticles** se identifican las tablas del usuario que tienen tablas de conflictos y se proporciona información sobre ellas.  
  
 De manera predeterminada, la información del conflicto se almacena:  
  
-   En el publicador y en el suscriptor, si el nivel de compatibilidad de la publicación es igual o superior a 90RTM.  
  
-   En el publicador, si el nivel de compatibilidad de la publicación es inferior a 80RTM.  
  
-   En el publicador, si los suscriptores utilizan [!INCLUDE[ssEW](../../../includes/ssew-md.md)]. No se pueden almacenar datos en conflicto en los suscriptores de [!INCLUDE[ssEW](../../../includes/ssew-md.md)] .  
  
 **Para ver conflictos**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Ver y resolver conflictos de datos para publicaciones de mezcla &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-and-resolve-data-conflicts-for-merge-publications.md)  
  
-   Programación de la replicación de [!INCLUDE[tsql](../../../includes/tsql-md.md)]: [Ver información de conflictos para publicaciones de mezcla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/view-conflict-information-for-merge-publications.md)  
  
## <a name="see-also"></a>Consulte también  
 [Sincronizar datos](../../../relational-databases/replication/synchronize-data.md)  
  
  
