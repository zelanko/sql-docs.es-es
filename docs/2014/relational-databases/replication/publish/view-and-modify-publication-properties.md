---
title: Ver y modificar propiedades de publicación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- modifying replication properties, articles
- articles [SQL Server replication], modifying
- publications [SQL Server replication], properties
- articles [SQL Server replication], properties
- modifying replication properties, publications
- publications [SQL Server replication], modifying
ms.assetid: 27d72ea4-bcb6-48f2-b4aa-eb1410da7efc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5053cc16734cc18c75e163fec4c06b1768e590cc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68941068"
---
# <a name="view-and-modify-publication-properties"></a>Ver y modificar propiedades de publicación
  En este tema se describe cómo ver y modificar las propiedades de publicación en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)]o Replication Management Objects (RMO).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para ver y modificar las propiedades de publicación con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Algunas propiedades no se pueden modificar después de crearlas, y otras no se pueden modificar si existen suscripciones a la publicación. Las propiedades que no se pueden modificar se muestran como de solo lectura.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Una vez creada una publicación, algunos cambios de las propiedades requieren una nueva instantánea. Si una publicación tiene suscripciones, algunos cambios también requieren reinicializar todas las suscripciones. Para más información, vea [Change Publication and Article Properties](change-publication-and-article-properties.md) (Cambiar las propiedades de la publicación y de los artículos) y [Agregar y quitar artículos de publicaciones existentes](add-articles-to-and-drop-articles-from-existing-publications.md).  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Vea y modifique propiedades de publicación en el cuadro de diálogo **Propiedades de la publicación: \<Publicación>** , que está disponible en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] y en el Monitor de replicación. Para información sobre cómo iniciar el Monitor de replicación, vea [Iniciar el Monitor de replicación](../monitor/start-the-replication-monitor.md).  
  
 En el cuadro de diálogo **Propiedades de la publicación: \<Publicación>** se incluyen las páginas siguientes:  
  
-   La página **General** incluye el nombre y la descripción de la publicación, el nombre de la base de datos, el tipo de publicación y los valores de expiración de la suscripción.  
  
-   La página **Artículos** corresponde a la página **Artículos** del Asistente para nueva publicación. Utilice esta página para agregar y eliminar artículos, y para cambiar propiedades y el filtro de columna de artículos.  
  
-   La página **Filtrar filas** corresponde a la página **Filtrar filas de tabla** del Asistente para nueva publicación. Utilice esta página para agregar, editar y eliminar filtros de fila estáticos de todos los tipos de publicaciones, y para agregar, editar y eliminar filtros de fila con parámetros y filtros de combinación de publicaciones de combinación.  
  
-   La página **Instantánea** permite especificar el formato y la ubicación de la instantánea, si la instantánea debe comprimirse y si los scripts deben ejecutarse antes y después de aplicar la instantánea.  
  
-   La página **Instantánea de FTP** (en publicaciones de instantáneas y transaccionales, y publicaciones de combinación en publicadores que ejecutan versiones anteriores a SQL Server 2005) permite especificar si los suscriptores pueden descargar archivos de instantáneas mediante el Protocolo de transferencia de archivos (FTP).  
  
-   La página **Instantánea de FTP e Internet** (en publicaciones de combinación de publicadores que ejecutan SQL Server 2005 o posterior) permite especificar si los suscriptores pueden descargar archivos de instantáneas mediante FTP y si los suscriptores pueden sincronizar suscripciones mediante HTTPS.  
  
-   La página **Opciones de suscripción** permite establecer diversas opciones que se aplican a todas las suscripciones. Las opciones varían según el tipo de publicación.  
  
-   La página **Lista de acceso a la publicación** permite especificar qué inicios de sesión y grupos pueden tener acceso a una publicación.  
  
-   La página **Seguridad del agente** le permite tener acceso a la configuración para las cuentas con las que se ejecutan los agentes siguientes y realizan conexiones a los equipos en una topología de replicación: el Agente de instantáneas para todas las publicaciones, el Agente de registro del LOG para todas las publicaciones transaccionales y el Agente de lectura de cola para las publicaciones transaccionales que permiten las suscripciones de actualización en cola.  
  
-   La página **Particiones de datos** (en publicaciones de combinación de publicadores que ejecutan SQL Server 2005 o posterior) permite especificar si los suscriptores a publicaciones con filtros con parámetros pueden solicitar una instantánea si no está disponible. También permite generar instantáneas de una o varias particiones, solo una vez o varias veces.  
  
#### <a name="to-view-and-modify-publication-properties-in-management-studio"></a>Para ver y modificar propiedades de una publicación en Management Studio  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]y luego expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic con el botón secundario en una publicación y, a continuación, haga clic en **Propiedades**.  
  
4.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
#### <a name="to-view-and-modify-publication-properties-in-replication-monitor"></a>Para ver y modificar propiedades de una publicación en el Monitor de replicación  
  
1.  Expanda un grupo de publicador en el panel izquierdo del Monitor de replicación y, a continuación, expanda un publicador.  
  
2.  Haga clic con el botón secundario en una publicación y, a continuación, haga clic en **Propiedades**.  
  
3.  Modifique las propiedades si es necesario y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Se puede modificar las publicaciones y devolver sus propiedades mediante programación utilizando procedimientos almacenados de replicación. Los procedimientos almacenados que utilice dependerán del tipo de publicación.  
  
#### <a name="to-view-the-properties-of-a-snapshot-or-transactional-publication"></a>Para ver las propiedades de una instantánea o publicación transaccional  
  
1.  Ejecute [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql), y especifique el nombre de la publicación para el parámetro **\@publication**. Si no especifica este parámetro, se devuelve información sobre todas las publicaciones del publicador.  
  
#### <a name="to-change-the-properties-of-a-snapshot-or-transactional-publication"></a>Para cambiar las propiedades de una instantánea o publicación transaccional  
  
1.  Ejecute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql), y especifique la propiedad de publicación que se va a cambiar en el parámetro **\@property** y el nuevo valor de esta propiedad en el parámetro **\@value**.  
  
    > [!NOTE]  
    >  Si el cambio va a requerir que se genere una instantánea nueva, también debe especificar el valor **1** para **\@force_invalidate_snapshot**, y si el cambio va a requerir que se reinicialicen los suscriptores, debe especificar el valor **1** para **\@force_reinit_subscription**. Para más información sobre las propiedades que, cuando se cambian, necesitan una nueva instantánea o una reinicialización, [Change Publication and Article Properties](change-publication-and-article-properties.md) (Cambiar las propiedades de la publicación y de los artículos).  
  
#### <a name="to-view-the-properties-of-a-merge-publication"></a>Para ver las propiedades de una publicación de combinación  
  
1.  Ejecute [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), y especifique el nombre de la publicación para el parámetro **\@publication**. Si no especifica este parámetro, se devuelve información sobre todas las publicaciones del publicador.  
  
#### <a name="to-change-the-properties-of-a-merge-publication"></a>Para cambiar las propiedades de una publicación de combinación  
  
1.  Ejecute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql), y especifique la propiedad de publicación que se va a cambiar en el parámetro **\@property** y el nuevo valor de esta propiedad en el parámetro **\@value**.  
  
    > [!NOTE]  
    >  Si el cambio va a requerir que se genere una instantánea nueva, también debe especificar el valor **1** para **\@force_invalidate_snapshot**, y si el cambio va a requerir que se reinicialicen los suscriptores, debe especificar el valor **1** para **\@force_reinit_subscription**. Para más información sobre las propiedades que, cuando se cambian, requieren una nueva instantánea o reinicialización, vea [Cambio de las propiedades de la publicación y de los artículos](change-publication-and-article-properties.md).  
  
#### <a name="to-view-the-properties-of-a-snapshot"></a>Para ver las propiedades de una instantánea  
  
1.  Ejecute [sp_helppublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql), y especifique el nombre de la publicación para el parámetro **\@publication**.  
  
#### <a name="to-change-the-properties-of-a-snapshot"></a>Para cambiar las propiedades de una instantánea  
  
1.  Ejecute [sp_changepublication_snapshot](/sql/relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql), especificando una o más de las nuevas propiedades de instantánea para los parámetros de instantánea adecuados.  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 Este ejemplo de replicación transaccional devuelve las propiedades de la publicación.  
  
 [!code-sql[HowTo#sp_helppublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranpub.sql#sp_helppublication)]  
  
 Este ejemplo de replicación transaccional deshabilita la replicación de esquema para la publicación.  
  
 [!code-sql[HowTo#sp_changepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changetranpub.sql#sp_changepublication)]  
  
 Este ejemplo de replicación de mezcla devuelve las propiedades de la publicación.  
  
 [!code-sql[HowTo#sp_helpmergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergepub.sql#sp_helpmergepublication)]  
  
 Este ejemplo de replicación de mezcla deshabilita la replicación de esquema para la publicación.  
  
 [!code-sql[HowTo#sp_changemergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/changemergepub.sql#sp_changemergepublication)]  
  
##  <a name="RMOProcedure"></a> Uso de Replication Management Objects (RMO)  
 Puede modificar publicaciones y obtener acceso mediante programación a sus propiedades utilizando Replication Management Objects (RMO). Las clases RMO que usa para ver o modificar las propiedades de publicación dependen del tipo de publicación.  
  
#### <a name="to-view-or-modify-properties-of-a-snapshot-or-transactional-publication"></a>Para ver o modificar las propiedades de una publicación transaccional o de instantáneas  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.TransPublication> , establezca las propiedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> y <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para la publicación y establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en la conexión creada en el paso 1.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve `false`, significa que las propiedades de publicación del paso 2 se definieron incorrectamente, o bien que la publicación no existe.  
  
4.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para una o más de las propiedades que se pueden establecer. Use el operador lógico AND (`&` en Microsoft Visual C# y `And` en Microsoft Visual Basic) para determinar si un valor <xref:Microsoft.SqlServer.Replication.PublicationAttributes> determinado está establecido para la propiedad <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>. (Opcional) Use el operador lógico OR inclusivo (`|` en Visual C# y `Or` en Visual Basic) y el operador lógico OR exclusivo (`^` en Visual C# y `Xor` en Visual Basic) para cambiar los valores <xref:Microsoft.SqlServer.Replication.PublicationAttributes> para la propiedad <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>.  
  
5.  (Opcional) Si especificara un valor de `true` para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar los cambios en el servidor. Si especificó el valor `false` para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (predeterminado), los cambios se envían inmediatamente al servidor.  
  
#### <a name="to-view-or-modify-properties-of-a-merge-publication"></a>Para ver o modificar las propiedades de una publicación de combinación  
  
1.  Cree una conexión al publicador mediante la clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Cree una instancia de la clase <xref:Microsoft.SqlServer.Replication.MergePublication> , establezca las propiedades <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> y <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> para la publicación y establezca la propiedad <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> en la conexión creada en el paso 1.  
  
3.  Llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obtener las propiedades del objeto. Si este método devuelve `false`, significa que las propiedades de publicación del paso 2 se definieron incorrectamente, o bien que la publicación no existe.  
  
4.  (Opcional) Para cambiar las propiedades, establezca un nuevo valor para una o más de las propiedades que se pueden establecer. Use el operador lógico AND (`&` en Visual C# y `And` en Visual Basic) para determinar si un valor <xref:Microsoft.SqlServer.Replication.PublicationAttributes> determinado está establecido para la propiedad <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>. (Opcional) Use el operador lógico OR inclusivo (`|` en Visual C# y `Or` en Visual Basic) y el operador lógico OR exclusivo (`^` en Visual C# y `Xor` en Visual Basic) para cambiar los valores <xref:Microsoft.SqlServer.Replication.PublicationAttributes> para la propiedad <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A>.  
  
5.  (Opcional) Si especificara un valor de `true` para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, llame al método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> para confirmar los cambios en el servidor. Si especificó el valor `false` para <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> (predeterminado), los cambios se envían inmediatamente al servidor.  
  
###  <a name="PShellExample"></a> Ejemplos (RMO)  
 Este ejemplo establece los atributos de publicación para una publicación transaccional. Los cambios están almacenados en memoria caché hasta que se envían explícitamente al servidor.  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeTranPub_cached](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changetranpub_cached)]  
  
 Este ejemplo deshabilita la replicación de DDL para una publicación de combinación.  
  
 [!code-csharp[HowTo#rmo_ChangeMergePub_ddl](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changemergepub_ddl)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergePub_ddl](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changemergepub_ddl)]  
  
## <a name="see-also"></a>Consulte también  
 [Publicar datos y objetos de base de datos](publish-data-and-database-objects.md)   
 [Cambiar las propiedades de la publicación y de los artículos](change-publication-and-article-properties.md)   
 [Realizar cambios de esquema en bases de datos de publicaciones](make-schema-changes-on-publication-databases.md)   
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Agregar y quitar artículos de una publicación](add-articles-to-and-drop-articles-from-a-publication.md)   
 [Visualización de información y realización de tareas mediante el Monitor de replicación](../monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [er y modificar las propiedades de un artículo](view-and-modify-article-properties.md)  
  
  
