---
title: Validar datos replicados | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- inline data validation [SQL Server replication]
- administering replication, validating data
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication]
- merge replication data validation [SQL Server replication], about data validation
- validating replicated data
ms.assetid: f7500a2b-61cb-41b5-816d-27609a6c58e7
caps.latest.revision: 45
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a57d074a1e24ec0d865c2a1be5c6a857ecb68354
ms.lasthandoff: 04/11/2017

---
# <a name="validate-replicated-data"></a>Validar datos replicados
  La replicación transaccional y la replicación de mezcla le permiten validar que los datos del suscriptor coinciden con los del publicador. Es posible realizar la validación de determinadas suscripciones o de todas las suscripciones a una publicación. Especifique uno de los siguientes tipos de validación y el Agente de distribución o el Agente de mezcla validarán los datos la próxima vez que se ejecuten:  
  
-   Solo de número de filas. Esta opción valida si la tabla del suscriptor tiene las mismas filas que la tabla del publicador pero no valida la coincidencia del contenido de las filas. La validación del recuento de filas proporciona una idea sobre validación que puede ponerle al corriente de problemas con los datos.  
  
-   Recuento de filas y suma de comprobación binaria. Además de llevar a cabo un recuento de filas en el publicador y en el suscriptor, se calcula una suma de comprobación de todos los datos utilizando el algoritmo de suma de comprobación. Si el número de filas da un error, no se lleva a cabo la suma de comprobación.  
  
 Además de validar que los datos en el suscriptor y en el publicador coincidan, la replicación de mezcla ofrece la posibilidad de validar que los datos presenten las particiones correctas para cada suscriptor. Para más información, vea [VValidar la información de particiones para un suscriptor de mezcla](../../relational-databases/replication/validate-partition-information-for-a-merge-subscriber.md).  
  
 **Para validar los datos**  
  
 Para validar todos los artículos de una suscripción, utilice [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], procedimientos almacenados o Replication Management Objects (RMO). Para más información, consulte [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md). Debe utilizar procedimientos almacenados para validar artículos individuales en publicaciones transaccionales y de instantáneas.  
  
## <a name="data-validation-results"></a>Resultados de la validación de datos  
 Cuando la validación se ha completado, el Agente de distribución o el Agente de mezcla registran mensajes sobre si ha sido correcta o se han producido errores (la replicación no informa sobre las filas que han dado error). Estos mensajes se pueden ver en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Monitor de replicación y en las tablas del sistema de replicación. En el tema de procedimientos indicado anteriormente se explica cómo ejecutar la validación y ver los resultados.  
  
 Para controlar errores de validación, tenga en cuenta lo siguiente:  
  
-   Configure la alerta de replicación **Replicación: el suscriptor no ha superado la validación de datos** para recibir una notificación del error. Para más información, vea [Configure Predefined Replication Alerts &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/administration/configure-predefined-replication-alerts-sql-server-management-studio.md) (Cómo configurar alertas de replicación predefinidas [SQL Server Management Studio]).  
  
-   ¿Son los errores de validación un problema para su aplicación? Si los errores de validación suponen un problema, actualice manualmente los datos para que se sincronicen o reinicialice la suscripción:  
  
    -   Los datos se pueden actualizar con la [utilidad tablediff](../../tools/tablediff-utility.md). Para más información sobre el uso de esta utilidad, vea [Compare Replicated Tables for Differences &#40;Replication Programming&#41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md) (Comparar tablas replicadas para buscar diferencias &#40;programación de la replicación&#41;).  
  
    -   Para más información sobre la reinicialización, vea [Reinitialize Subscriptions](../../relational-databases/replication/reinitialize-subscriptions.md) (Reinicializar suscripciones).  
  
## <a name="considerations-for-data-validation"></a>Consideraciones sobre la validación de datos  
 Tenga en cuenta las siguientes cuestiones a la hora de validar los datos:  
  
-   Debe detener todas las actividades de actualización en los suscriptores antes de validar los datos (no es necesario detener todas las actividades en el publicador durante la validación).  
  
-   Dado que las sumas de comprobación y las sumas de comprobación binarias requieren grandes cantidades de recursos del procesador para validar un conjunto de datos de gran tamaño, debe programar la validación para que se produzca cuando la actividad sea mínima en los servidores que se utilizan en la replicación.  
  
-   La replicación solo valida tablas; no valida si los artículos solo de esquema (como los procedimientos almacenados) son iguales en el publicador y en el suscriptor.  
  
-   La suma de comprobación binaria se puede utilizar en cualquier tabla publicada. La suma de comprobación no puede validar tablas con filtros de columna ni estructuras de tabla lógicas donde los desplazamientos de columnas son distintos (debido a las instrucciones ALTER TABLE que quitan o agregan columnas).  
  
-   La validación de replicación usa las funciones **checksum** y **binary_checksum** . Para obtener información sobre este comportamiento, vea [CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md) y [BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md).  
  
-   La validación mediante suma de comprobación binaria o suma de comprobación puede informar incorrectamente sobre un error si los tipos de datos son diferentes en el suscriptor y en el publicador. Esto se puede producir si lleva a cabo una de las siguientes acciones:  
  
    -   Establecer de forma explícita opciones del esquema para asignar tipos de datos de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Establecer el nivel de compatibilidad de la publicación de una publicación de combinación en una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cuando las tablas publicadas contienen uno o más tipos de datos que se deben asignados a esta versión.  
  
    -   Inicializar de forma manual una suscripción, si usa diferentes tipos de datos en el suscriptor.  
  
-   Las validaciones de suma de comprobación binaria y de suma de comprobación no son compatibles con suscripciones transformables en la replicación transaccional.  
  
-   La validación no se admite para los datos replicados en suscriptores que no son de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="how-data-validation-works"></a>Cómo funciona la validación de datos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida los datos calculando un recuento de filas o una suma de comprobación en el Publicador y, a continuación, compara estos valores con el recuento de filas o suma de comprobación calculado en el suscriptor. Se calcula un valor para toda la tabla de publicación y otro valor para toda la tabla de suscripción, pero en los cálculos no se incluyen los datos de las columnas **text**, **ntext**ni **image** .  
  
 Mientras se realizan los cálculos, se colocan bloqueos compartidos temporalmente en las tablas en las que se ejecutan los recuentos de filas y sumas de comprobación, pero los cálculos se completan rápidamente y los bloqueos compartidos se quitan normalmente en unos segundos.  
  
 Cuando se utilizan sumas de comprobación binarias, se produce una comprobación de redundancia cíclica (CRC) de 32 bits columna por columna en vez de una comprobación CRC en la fila física de la página de datos. Esto permite que las columnas de la tabla estén en cualquier orden físicamente en la página de datos, pero se calcula la misma comprobación CRC para la fila. Es posible utilizar la validación de suma de comprobación binaria cuando hay filtros de fila o de columna en la publicación.  
  
## <a name="see-also"></a>Vea también  
 [Best Practices for Replication Administration](../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
