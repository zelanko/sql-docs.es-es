---
title: "Replicación en suscriptores de tablas con optimización para memoria | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 11/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eda94d43e65319f152ea387372c5f28193697818
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>Replicación en suscriptores de tablas con optimización para memoria
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Las tablas que actúan como instantáneas y suscriptores de replicación transaccional, excluida la replicación transaccional punto a punto, pueden configurarse como tablas optimizadas para memoria. Otras configuraciones de replicación no son compatibles con las tablas optimizadas para memoria. Esta característica está disponible a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].  
  
## <a name="two-configurations-are-required"></a>Son necesarias dos configuraciones  
  
-   
            **Configurar la base de datos de suscriptor para admitir la replicación a tablas optimizadas para memoria**  
  
     Establezca la propiedad **@memory_optimized** en **true** mediante [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) o [sp_changesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md).  
  
-   
            **Configurar el artículo para admitir la replicación a tablas optimizadas para memoria**  
  
     Establezca la opción `@schema_option = 0x40000000000` para el artículo mediante [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) o [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md).  
  
#### <a name="to-configure-a-memory-optimized-table-as-a-subscriber"></a>Para configurar una tabla optimizada para memoria como suscriptor  
  
1.  Cree una publicación transaccional. Para más información, consulte [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Agregue artículos a la publicación. Para más información, consulte [Define an Article](../../relational-databases/replication/publish/define-an-article.md).  
  
     Si la configuración se realiza mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] set the **@schema_option** del procedimiento almacenado **sp_addarticle** en   
    **0x40000000000**.  
  
3.  En la ventana de propiedades del artículo, establezca **Habilitar optimización para memoria** en **true**.  
  
4.  Inicie el trabajo del Agente de instantáneas para generar la instantánea inicial de esta publicación. Para más información, consulte [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
5.  Ahora cree una nueva suscripción. En el **Asistente para nueva suscripción** , establezca **Memory Optimized Subscription** (Suscripción optimizada para memoria) en **true**.  
  
 Las tablas con optimización para memoria deben empezar ahora a recibir actualizaciones del publicador.  
  
#### <a name="reconfigure-an-existing-transaction-replication"></a>Reconfiguración de una replicación de transacción existente  
  
1.  Vaya a las propiedades de suscripción de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y establezca **Memory Optimized Subscription** (Suscripción optimizada para memoria) en **true**. Los cambios no se aplican hasta que se reinicializa la suscripción.  
  
     Si la configuración se realiza mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] , establezca el nuevo parámetro **@memory_optimized** del procedimiento almacenado **sp_addsubscription** en true.  
  
2.  Vaya a las propiedades del artículo de una publicación en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y establezca **Enable Memory Optimization** (Habilitar optimización para memoria) en true.  
  
     Si la configuración se realiza mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] set the **@schema_option** del procedimiento almacenado **sp_addarticle** en   
    **0x40000000000**.  
  
3.  Las tablas con optimización para memoria no admiten índices agrupados. Para hacer posible esto, la replicación los convierte en índices no agrupados estableciendo **Convert clustered index to nonclustered for memory optimized article** (Convertir índice agrupado en no agrupado para un artículo optimizado para memoria) en true.  
  
     Si la configuración se realiza mediante [!INCLUDE[tsql](../../includes/tsql-md.md)] set the **@schema_option** del procedimiento almacenado **sp_addarticle** en  **0x0000080000000000**.  
  
4.  Vuelva a generar la instantánea.  
  
5.  Reinicialice la suscripción.  
  
## <a name="remarks-and-restrictions"></a>Comentarios y restricciones  
 Solo se admite la replicación transaccional unidireccional. No se admite la replicación transaccional punto a punto.  
  
 Las tablas con optimización para memoria no se pueden publicar.  
  
 Las tablas de replicación del distribuidor no se pueden configurar como tablas optimizadas para memoria.  
  
 La replicación de mezcla no puede incluir tablas optimizadas para memoria.  
  
 En el suscriptor, las tablas implicadas en la replicación transaccional se pueden configurar como tablas optimizadas para memoria, pero las tablas del suscriptor deben cumplir los requisitos de las tablas optimizadas para memoria. Esto requiere las restricciones siguientes.  
 
-   Las tablas replicadas en tablas optimizadas para memoria de un suscriptor están limitadas a los tipos de datos permitidos en las tablas optimizadas para memoria. Para obtener más información, vea [Tipos de datos admitidos para OLTP en memoria](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md).  
  
-   No todas las características de Transact-SQL son compatibles con las tablas optimizadas en memoria. Vea [Transact-SQL Constructs Not Supported by In-Memory OLTP](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) para obtener información detallada.  
  
##  <a name="Schema"></a> Modificar un archivo de esquema  
  
-   Si se usa la opción `DURABILITY = SCHEMA_AND_DATA` de tabla optimizada para memoria, la tabla debe tener un índice de clave principal no clúster.  
  
-   ANSI_PADDING debe ser ON.  
  
## <a name="see-also"></a>Vea también  
 [Características y tareas de replicación](../../relational-databases/replication/replication-features-and-tasks.md)  
  
  
