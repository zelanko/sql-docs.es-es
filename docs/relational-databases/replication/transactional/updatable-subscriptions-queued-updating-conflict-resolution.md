---
title: Detección y resolución de conflictos de actualización en cola | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- viewing queued updating conflicts
- conflict resolution [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
- articles [SQL Server replication], conflict resolution
ms.assetid: 084ac587-25e7-4bd0-a385-556bbe07d02f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9364de40aed4218d1abf73dac1502413c3509edf
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883206"
---
# <a name="updatable-subscriptions---queued-updating-conflict-resolution"></a>Suscripciones actualizables: Resolución de conflictos de actualización en cola
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Como las suscripciones de actualización en cola permiten realizar modificaciones en los mismos datos en múltiples ubicaciones, pueden producirse conflictos cuando se sincronizan los datos en el publicador. La replicación detecta los conflictos cuando se sincronizan los cambios con el publicador y resuelve esos conflictos utilizando la directiva de resolución que ha seleccionado al crear la publicación. Pueden producirse los siguientes conflictos:  
  
-   Conflictos de actualización e inserción. Tienen lugar cuando se modifican los mismos datos en dos ubicaciones. Una de las modificaciones "gana", mientras que la otra "pierde".  
  
-   Conflictos de eliminación. Ocurren cuando se elimina una fila en una ubicación y se modifica la misma fila en otra.  
  
 La detección y resolución de conflictos puede consumir mucho tiempo y muchos recursos y, por tanto, es mejor minimizar los conflictos de la aplicación creando particiones de datos de forma que los distintos suscriptores modifiquen distintos subconjuntos de datos.  
  
## <a name="detecting-conflicts"></a>Detectar conflictos  
 Al crear una publicación y habilitar la actualización en cola, la replicación agrega una columna **uniqueidentifier** (**msrepl_tran_version**) con el valor predeterminado **newid()** en la tabla subyacente. Cuando se modifican los datos publicados en el publicador o el suscriptor, la fila recibe un identificador único global (GUID) para indicar que existe una nueva versión de la fila. El Agente de lectura de cola utiliza esta columna durante la sincronización para determinar si existe un conflicto.  
  
 Una transacción en cola mantiene los valores de versión nuevo y antiguo. Cuando la transacción se aplica en el publicador, se comparan los GUID de la transacción y el GUID de la publicación. Si el GUID almacenado en la transacción coincide con el GUID de la publicación, la publicación se actualiza y se asigna a la fila el nuevo GUID generado por el suscriptor. Al actualizar la publicación con el GUID de la transacción, tendrá versiones de fila coincidentes en la publicación y en la transacción.  
  
 Si el GUID antiguo almacenado en la transacción no coincide con el de la publicación, se detectará un conflicto. El nuevo GUID de la publicación indica que existen dos versiones diferentes de la fila: una en la transacción enviada por el suscriptor y otra más reciente que existe en el publicador. En este caso, otro suscriptor o publicador actualizó la misma fila en la publicación antes de la sincronización de esta transacción de suscriptor.  
  
 A diferencia de la replicación de mezcla, no se utiliza una columna GUID para identificar la fila, sino para comprobar si la fila ha cambiado.  
  
## <a name="resolving-conflicts"></a>Solucionar conflictos  
 Al crear una publicación con la actualización en cola, se selecciona un solucionador de conflictos que se utilizará si se detectan conflictos. El solucionador de conflictos rige la forma en que el Agente de lectura de cola controla diferentes versiones de la misma fila que se encuentran durante la sincronización. Puede modificar la directiva de resolución de conflictos después de crear la publicación, con tal de que no haya suscripciones a la publicación. Las opciones del solucionador de conflictos son las siguientes:  
  
-   El publicador gana (valor predeterminado)  
  
-   El publicador gana y se reinicializa la suscripción  
  
-   El suscriptor gana  
  
 Los conflictos se registran y se pueden ver con el Visor de conflictos.  
  
 **Para establecer la directiva de resolución de conflictos de actualización en cola**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Establecer opciones de resolución de conflictos de actualización en cola &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
-   Programación de la replicación con Transact-SQL: [Habilitar suscripciones actualizables para publicaciones transaccionales](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
 **Para ver conflictos de datos**  
  
-   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]: [Ver conflictos de datos para publicaciones transaccionales &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/view-data-conflicts-for-transactional-publications-sql-server-management-studio.md)  
  
### <a name="publisher-wins"></a>El publicador gana  
 Cuando la resolución de conflictos se establece en El publicador gana, se mantiene la coherencia transaccional en función de los datos del publicador. La transacción en conflicto se revierte en el suscriptor que la inició.  
  
 El Agente de lectura de cola detecta un conflicto y se generan y propagan al suscriptor comandos de compensación; para ello, se publican en la base de datos de distribución. A continuación, el Agente de distribución aplica los comandos de compensación al suscriptor que originó la transacción en conflicto. Las acciones de compensación actualizan las filas en el suscriptor, de forma que coincidan con las filas del publicador.  
  
 Hasta que se apliquen los comandos de compensación será posible leer los resultados de una transacción que finalmente se revertirá en el suscriptor. Esto equivale a una lectura no actualizada (nivel de aislamiento de lectura no confirmada). No habrá compensación para las siguientes transacciones dependientes que puedan producirse. Sin embargo, se garantizan los límites de la transacción y todas las acciones de una transacción se confirman o, en caso de conflicto, se revierten.  
  
### <a name="publisher-wins-and-the-subscription-is-reinitialized"></a>El publicador gana y se reinicializa la suscripción  
 La opción de reinicializar el suscriptor para solucionar conflictos mantiene una coherencia estricta en el suscriptor, pero puede consumir mucho tiempo si la publicación contiene grandes cantidades de datos.  
  
 Cuando el Agente de lectura de cola detecta un conflicto, se rechazan las demás transacciones de la cola (incluida la transacción en conflicto) y se marca el suscriptor para su reinicialización. El Agente de distribución aplica al suscriptor la siguiente instantánea generada para la publicación.  
  
### <a name="subscriber-wins"></a>El suscriptor gana  
 La detección de conflictos con la directiva El suscriptor gana significa que la última transacción de suscriptor que actualice el publicador ganará. En este caso, cuando se detecte un conflicto, se seguirá utilizando la transacción enviada por el suscriptor y se actualizará el publicador. Esta directiva es apropiada para las aplicaciones en que estos cambios no pongan en peligro la integridad de los datos.  
  
## <a name="see-also"></a>Consulte también  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  
