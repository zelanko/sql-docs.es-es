---
title: Realización de cambios de esquema en bases de datos de publicación | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], schema changes
- snapshot replication [SQL Server], replicating schema changes
- merge replication [SQL Server replication], replicating schema changes
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
- publishing [SQL Server replication], schema changes
ms.assetid: 926c88d7-a844-402f-bcb9-db49e5013b69
caps.latest.revision: 73
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 905725cecea8e2dee08641b49500d23f664f934b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32965340"
---
# <a name="make-schema-changes-on-publication-databases"></a>Realizar cambios de esquema en bases de datos de publicaciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replicación admite una gran variedad de cambios en el esquema de objetos publicados. Cuando se realiza cualquiera de los siguientes cambios de esquema en el objeto publicado apropiado en un publicador de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , dicho cambio se propaga de manera predeterminada a todos los suscriptores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   ALTER TABLE  
  
-   ALTER TABLE SET LOCK ESCALATION no se debe usar si la replicación de cambio de esquema está habilitada y una topología incluye suscriptores [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o [!INCLUDE[ssEWnoversion](../../../includes/ssewnoversion-md.md)].

-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
     ALTER TRIGGER solo puede utilizarse para desencadenadores de lenguaje de manipulación de datos (DML), ya que los desencadenadores de lenguaje de definición de datos (DDL) no se pueden replicar.  
  
> [!IMPORTANT]  
>  Los cambios de esquema de las tablas deben realizarse con [!INCLUDE[tsql](../../../includes/tsql-md.md)] u Objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO). Cuando se realizan cambios de esquema en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] intenta quitar y volver a crear la tabla. Debido a que no es posible quitar objetos publicados, se produce un error en el cambio de esquema.  
  
 En la replicación transaccional y de mezcla, los cambios de esquema se propagan de forma incremental al ejecutar el Agente de distribución o el Agente de mezcla. En la replicación de instantáneas, los cambios de esquema se propagan al aplicar una nueva instantánea en el suscriptor. En la replicación de instantáneas, se envía una nueva copia del esquema al suscriptor cada vez que se produce la sincronización. Por tanto, todos los cambios de esquema (y no solo los indicados antes) en objetos previamente publicados se propagan automáticamente con cada sincronización.  
  
 Para obtener información sobre cómo agregar y quitar artículos de publicaciones, vea [Agregar y quitar artículos de publicaciones existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
 **Para replicar cambios de esquema**  
  
 Los cambios de esquema antes indicados se replican de manera predeterminada. Para obtener información acerca de cómo deshabilitar la replicación de los cambios de esquema, vea [Replicate Schema Changes](../../../relational-databases/replication/publish/replicate-schema-changes.md).  
  
## <a name="considerations-for-schema-changes"></a>Consideraciones para los cambios de esquema  
 Tenga en cuenta las consideraciones siguientes al replicar cambios de esquema.  
  
### <a name="general-considerations"></a>Consideraciones generales  
  
-   Los cambios de esquema están sujetos a las restricciones impuestas por [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Por ejemplo, ALTER TABLE no permite aplicar ALTER a las columnas de clave principal.  
  
-   La asignación de tipo de datos solo se realiza para la instantánea inicial. Los cambios de esquema no se asignan a versiones anteriores de tipos de datos. Por ejemplo, si la instrucción `ALTER TABLE ADD datetime2 column` se utiliza en [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], el tipo de datos no se traduce a **nvarchar** para los suscriptores de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] . En algunos casos, los cambios de esquema se bloquean en el publicador.  
  
-   Si una publicación está configurada para permitir la propagación de los cambios de esquema, éstos se propagarán independientemente de cómo esté establecida la opción de esquema relacionada para un artículo de la publicación. Por ejemplo, si elige no replicar las restricciones de clave externa para un artículo de la tabla y después emite un comando ALTER TABLE que agrega una clave externa a la tabla en el publicador, la clave externa se agregará a la tabla en el suscriptor. Para evitarlo, deshabilite la propagación de los cambios de esquema antes de emitir el comando ALTER TABLE.  
  
-   Los cambios de esquema deben realizarse únicamente en el publicador y no en los suscriptores (incluidos los suscriptores de republicación). La replicación de mezcla impide los cambios de esquema en el suscriptor. La replicación transaccional no impide los cambios, pero los cambios pueden causar errores en la replicación.  
  
-   Los cambios propagados a un suscriptor de republicación se propagan de manera predeterminada a sus suscriptores.  
  
-   Si el cambio de esquema hace referencia a objetos o restricciones existentes en el publicador, pero no en el suscriptor, el cambio de esquema se realizará correctamente en el publicador pero se producirá un error en el suscriptor.  
  
-   Todos los objetos del suscriptor a los que se hace referencia al agregar una clave externa deben tener el mismo nombre y propietario que el objeto correspondiente en el publicador.  
  
-   No se permite agregar, quitar ni alterar índices explícitamente. Se admiten los índices creados implícitamente para las restricciones (como la restricción de clave principal).  
  
-   No se permite alterar ni quitar columnas de identidad administradas por la replicación. Para obtener más información sobre la administración automática de las columnas de identidad, vea [Replicar columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
-   No se admiten los cambios de esquema que incluyen funciones no deterministas, ya que pueden producir datos distintos en el publicador y en el suscriptor (falta de convergencia). Por ejemplo, si emite en el publicador el comando `ALTER TABLE SalesOrderDetail ADD OrderDate DATETIME DEFAULT GETDATE()`, los valores serán distintos cuando el comando se replique en el suscriptor y se ejecute. Para obtener más información acerca de las funciones no deterministas, vea [Deterministic and Nondeterministic Functions](../../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
-   Se recomienda asignar explícitamente un nombre a las restricciones. Si una restricción no tiene un nombre explícito, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera un nombre para la restricción y estos nombres serán diferentes en el publicador y en cada suscriptor. Esto puede causar problemas durante la replicación de cambios de esquema. Por ejemplo, si quita una columna en el publicador y se quita una restricción dependiente, la replicación intentará quitar la restricción en el suscriptor. Esta eliminación en el suscriptor no se podrá llevar a cabo porque el nombre de la restricción es diferente. Si no funciona la sincronización por un problema de nombre de restricción, quite manualmente la restricción en el suscriptor y ejecute de nuevo el agente de mezcla.  
  
-   Si se publica una tabla para la replicación, no se puede modificar una columna de esa tabla a un tipo de datos de XML si ya se ha generado una instantánea de publicación. Para modificar la columna, antes debe quitar la replicación.  
  
-   La lectura no confirmada no es un nivel de aislamiento compatible al hacer DDL en una tabla publicada.  
  
-   No se debe usar**SET CONTEXT_INFO** para modificar el contexto de las transacciones en las que se realizan cambios de esquema en objetos publicados.  
  
#### <a name="adding-columns"></a>Agregar columnas  
  
-   Para agregar una columna nueva a una tabla e incluirla en una publicación existente, ejecute ALTER TABLE \<tabla> ADD \<columna>. De manera predeterminada, la columna se replicará en todos los suscriptores. La columna debe admitir valores NULL o incluir una restricción predeterminada. Para obtener más información sobre la forma de agregar columnas, consulte la sección "Replicación de mezcla" de este tema.  
  
-   Para agregar una columna nueva a una tabla sin incluirla en una publicación existente, deshabilite la replicación de los cambios de esquema y después, ejecute ALTER TABLE \<tabla> ADD \<columna>.  
  
-   Para incluir una columna existente en una publicación existente, use [sp_articlecolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), [sp_mergearticlecolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) o el cuadro de diálogo **Propiedades de la publicación: \<publicación>**.  
  
     Para más información, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md). Será necesario reinicializar las suscripciones.  
  
-   No se admite la posibilidad de agregar una columna de identidad a una tabla publicada porque puede dar como resultado la falta de convergencia cuando la columna se replica en el suscriptor. Los valores de la columna de identidad en el publicador dependen del orden en que se almacenen físicamente las filas de la tabla afectada. Las filas se pueden almacenar de forma diferente en el suscriptor; por tanto, el valor de la columna de identidad puede ser diferente para las mismas filas.  
  
#### <a name="dropping-columns"></a>Quitar columnas  
  
-   Para quitar una columna de una publicación existente y de la tabla del publicador, ejecute ALTER TABLE \<tabla> DROP \<columna>. De forma predeterminada, la columna se quitará de la tabla en todos los suscriptores.  
  
-   Para quitar una columna de una publicación existente, pero conservarla en la tabla del publicador, use [sp_articlecolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), [sp_mergearticlecolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) o el cuadro de diálogo **Propiedades de la publicación: \<publicación>**.  
  
     Para más información, consulte [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md). Será necesario generar una instantánea nueva.  
  
-   La columna que se quita no puede utilizarse en las cláusulas de filtro de ningún artículo de ninguna publicación de la base de datos.  
  
-   Al quitar una columna de un artículo publicado, tenga en cuenta las restricciones, índices o propiedades de la columna que pudieran afectar a la base de datos. Por ejemplo:  
  
    -   No puede quitar columnas utilizadas en una clave principal de los artículos en publicaciones transaccionales, ya que se utilizan en la replicación.  
  
    -   No puede quitar la columna rowguid de los artículos de publicaciones de combinación ni la columna mstran_repl_version de los artículos de publicaciones transaccionales que admiten suscripciones de actualización, ya que se usan en la replicación.  
  
    -   Los cambios de índice no se propagan a los suscriptores: si quita una columna en el publicador y se quita un índice dependiente, la eliminación del índice no se replica. Debe quitar el índice en el suscriptor antes de quitar la columna en el publicador, de manera que se lleve a cabo correctamente la eliminación de la columna cuando se replique desde el publicador al suscriptor. Si no funciona la sincronización debido a un índice en el suscriptor, quite manualmente el índice y ejecute de nuevo el agente de mezcla.  
  
    -   Las restricciones deben tener un nombre explícito para permitir la eliminación. Para obtener más información, vea la sección "Consideraciones generales" de este tema.  
  
### <a name="transactional-replication"></a>replicación transaccional  
  
-   Los cambios de esquema se propagan a los suscriptores que ejecutan versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], pero la instrucción DDL solo debe incluir sintaxis compatible con la versión instalada en el suscriptor.  
  
     Si el suscriptor vuelve a publicar los datos, los únicos cambios de esquema admitidos serán agregar y quitar una columna. Estos cambios deberían realizarse en el publicador mediante [sp_repladdcolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) y [sp_repldropcolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md) en lugar de mediante la sintaxis ALTER TABLE DDL.  
  
-   Los cambios de esquema no se replican en los suscriptores que no sean de SQL Server.  
  
-   Los cambios de esquema no se propagan desde los publicadores que no sean de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   No se pueden alterar las vistas indizadas que se replican como tablas. Se pueden alterar las vistas indizadas que se replican como tales, pero esto hará que se conviertan en vistas normales en lugar de vistas indizadas.  
  
-   Si la publicación admite suscripciones de actualización inmediata o en cola, se debe poner el sistema en modo inactivo antes de realizar cambios de esquema: es necesario detener toda la actividad en la tabla publicada en el publicador y los suscriptores, y propagar los datos pendientes a todos los nodos. Una vez propagados los cambios de esquema a todos los nodos, se puede reiniciar la actividad en las tablas publicadas.  
  
-   Si la publicación está en una topología punto a punto, se debe poner el sistema en modo inactivo antes de realizar cambios de esquema. Para más información, vea [Poner en modo inactivo una topología de replicación &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md).  
  
-   La adición de una columna de marca de tiempo a una tabla y la asignación de la marca de tiempo a binary(8) hacen que se reinicialice el artículo para todas las suscripciones activas.  
  
### <a name="merge-replication"></a>Replicación de mezcla  
  
-   El nivel de compatibilidad de las publicaciones determina la forma en que la replicación de mezcla controla los cambios de esquema y si la instantánea debe establecerse en modo nativo (valor predeterminado) o en modo de carácter:  
  
    -   Para replicar cambios de esquema, el nivel de compatibilidad de la publicación debe ser de al menos 90RTM. Si los suscriptores ejecutan versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o el nivel de compatibilidad es inferior a 90RTM, puede usar [sp_repladdcolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) y [sp_repldropcolumn &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md) para agregar y quitar columnas. No obstante, estos procedimientos están desusados.  
  
    -   Si intenta agregar a un artículo existente una columna con un tipo de datos introducido en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se comportará de este modo:  
  
        ||100RTM, instantánea nativa|100RTM, instantánea de carácter|Todos los demás niveles de compatibilidad|  
        |-|-----------------------------|--------------------------------|------------------------------------|  
        |**hierarchyid**|Permitir cambio|Bloquear cambio|Bloquear cambio|  
        |**geography** y **geometry**|Permitir cambio|Permitir cambio*|Bloquear cambio|  
        |**secuencia de archivo**|Permitir cambio|Bloquear cambio|Bloquear cambio|  
        |**date**, **time**, **datetime2**y **datetimeoffset**|Permitir cambio|Permitir cambio*|Bloquear cambio|  
  
         *Los suscriptores de SQL Server Compact convierten estos tipos de datos en el suscriptor.  
  
-   En caso de error al aplicar un cambio de esquema (por ejemplo, un error que se produce por agregar una clave externa que hace referencia a una tabla que no está disponible en el suscriptor), se produce un error en la sincronización y es necesario reinicializar la suscripción.  
  
-   Si se realiza un cambio de esquema en una columna que forma parte de un filtro de combinación o con parámetros, es necesario reinicializar todas las suscripciones y volver a generar la instantánea.  
  
-   La replicación de mezcla proporciona procedimientos almacenados para omitir los cambios de esquema durante la solución de problemas. Para obtener más información, vea [sp_markpendingschemachange &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md) y [sp_enumeratependingschemachanges &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md).  
  
## <a name="see-also"></a>Ver también  
 [ALTER TABLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER VIEW &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-view-transact-sql.md)   
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-procedure-transact-sql.md)   
 [ALTER FUNCTION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-function-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Volver a generar procedimientos transaccionales personalizados para reflejar cambios de esquema](../../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)  
  
  
