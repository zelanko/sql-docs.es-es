---
title: Publicación de datos y objetos de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- user-defined types [SQL Server replication]
- articles [SQL Server replication], dropping
- objects [SQL Server replication]
- publications [SQL Server replication], creating
- merge replication [SQL Server replication], publications
- schema-only articles [SQL Server replication]
- publishing [SQL Server replication], database objects
- articles [SQL Server replication], defining
- publishing [SQL Server replication], functions
- replication [SQL Server], publications
- publishing [SQL Server replication], views
- tables [SQL Server replication]
- schemas [SQL Server replication]
- publishing [SQL Server replication], data
- schemas [SQL Server replication], publishing
- articles [SQL Server replication], stored procedures and
- publishing [SQL Server replication], tables
- alias data types [SQL Server replication]
- publications [SQL Server replication], deleting
- snapshot replication [SQL Server], publications
- articles [SQL Server replication], modifying
- transactional replication, publications
- publishing [SQL Server replication], stored procedures
- publishing [SQL Server replication]
- views [SQL Server replication]
- stored procedures [SQL Server replication], publishing
- publications [SQL Server replication], schema options
- articles [SQL Server replication], adding
- publications [SQL Server replication], modifying
- user-defined functions [SQL Server replication]
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
caps.latest.revision: 83
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 561892a92165e228496e771d869d8e86a0b656c9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="publish-data-and-database-objects"></a>Publicar datos y objetos de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Al crear una publicación puede elegir las tablas y otros objetos de base de datos que desee publicar. Puede publicar los siguientes objetos de base de datos utilizando la replicación.  
  
|Objeto de base de datos|Replicación de instantáneas y replicación transaccional|Replicación de mezcla|  
|---------------------|--------------------------------------------------------|-----------------------|  
|Tablas|X|X|  
|Tablas con particiones|X|X|  
|Procedimientos almacenados: definición ([!INCLUDE[tsql](../../../includes/tsql-md.md)] y CLR)|X|X|  
|Procedimientos almacenados: ejecución ([!INCLUDE[tsql](../../../includes/tsql-md.md)] y CLR)|X|no|  
|Vistas|X|X|  
|Vistas indizadas|X|X|  
|Vista indizadas como tablas|X|no|  
|Tipos definidos por el usuario (CLR)|X|X|  
|Funciones definidas por el usuario ([!INCLUDE[tsql](../../../includes/tsql-md.md)] y CLR)|X|X|  
|Tipos de datos de alias|X|X|  
|Índices de texto completo|X|X|  
|Objetos de esquema (restricciones, índices, desencadenadores DML de usuario, propiedades extendidas e intercalación)|X|X|  
  
## <a name="creating-publications"></a>Crear publicaciones  
 Para crear una publicación, debe proporcionar la siguiente información:  
  
-   El distribuidor.  
  
-   La ubicación de los archivos de instantáneas.  
  
-   La base de datos de publicaciones.  
  
-   El tipo de publicación que se va a crear (de instantánea, transaccional, transaccional con suscripciones actualizables o de mezcla).  
  
-   Los datos y los objetos de la base de datos (artículos) que se incluirán en la publicación.  
  
-   Filtros de fila estáticos y filtros de columna para todos los tipos de publicaciones, y filtros de fila con parámetros y filtros de combinación para publicaciones de combinación.  
  
-   La programación del Agente de instantáneas.  
  
-   Las cuentas con las que se ejecutarán los siguientes agentes: el Agente de instantáneas para todas las publicaciones, el Agente de registro del LOG para todas las publicaciones transaccionales, el Agente de lectura de cola para publicaciones transaccionales que permiten suscripciones de actualización.  
  
-   Un nombre y una descripción para la publicación.  
  
 Para obtener información acerca de cómo trabajar con publicaciones, vea los siguientes temas:  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Definir un artículo](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [er y modificar las propiedades de un artículo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [Eliminar una publicación](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [Eliminar un artículo](../../../relational-databases/replication/publish/delete-an-article.md)  
  
> [!NOTE]  
>  Al eliminar un artículo o una publicación, los objetos no se quitan del suscriptor.  
  
## <a name="publishing-tables"></a>Publicar tablas  
 El objeto que se publica con más frecuencia es la tabla. Los siguientes vínculos proporcionan información adicional acerca de las áreas relacionadas con la publicación de tablas:  
  
-   [Filtrar datos publicados](../../../relational-databases/replication/publish/filter-published-data.md)  
  
-   [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
-   [Article Options for Merge Replication](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  
  
-   [Replicar columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
 Cuando se publica una tabla para replicación, puede especificar qué objetos de esquema se deben copiar al suscriptor, como la integridad referencial declarada (restricciones de clave principal, de referencia y UNIQUE), los índices, los desencadenadores DML de usuario (los desencadenadores DDL no se pueden replicar), las propiedades extendidas y la intercalación. Las propiedades extendidas solo se replican en la sincronización inicial entre el publicador y el suscriptor. Si agrega o modifica una propiedad extendida después de la sincronización inicial, el cambio no se replica.  
  
 Para especificar opciones de esquema, vea [Especificar las opciones del esquema](../../../relational-databases/replication/publish/specify-schema-options.md) o <xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>.  
  
### <a name="partitioned-tables-and-indexes"></a>Partitioned Tables and Indexes  
 La replicación admite la publicación de tablas con particiones e índices. El nivel de compatibilidad depende del tipo de replicación que se utiliza y las opciones que especifica para la publicación y los artículos asociados a las tablas con particiones. Para obtener más información, vea [Replicar tablas e índices con particiones](../../../relational-databases/replication/publish/replicate-partitioned-tables-and-indexes.md).  
  
## <a name="publishing-stored-procedures"></a>Publicar procedimientos almacenados  
 Todos los tipos de replicación permiten replicar definiciones de procedimientos almacenados: CREATE PROCEDURE se copia en cada suscriptor. En el caso de los procedimientos almacenados CLR (Common Language Runtime), también se copia el ensamblado asociado. Los cambios en los procedimientos se replican en los suscriptores, a diferencia de los cambios en los ensamblados asociados.  
  
 Además de replicar la definición de un procedimiento almacenado, la replicación transaccional permite replicar la ejecución de procedimientos almacenados. Esto resulta de utilidad al replicar los resultados de los procedimientos almacenados orientados al mantenimiento que afectan a grandes cantidades de datos. Para obtener más información, consulte [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md).  
  
## <a name="publishing-views"></a>Publicar vistas  
 Todos los tipos de replicación permiten replicar vistas: la vista (y el índice asociado, si se trata de una vista indizada) se puede copiar en el suscriptor, pero la tabla base también se debe replicar.  
  
 En las vistas indizadas, la replicación transaccional también permite replicar la vista indizada en forma de tabla y no como vista, eliminando la necesidad de replicar también la tabla base. Para ello, especifique una de las opciones "indexed view logbased" del parámetro *@type* de [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Para obtener más información sobre cómo usar **sp_addarticle**, vea [Definir un artículo](../../../relational-databases/replication/publish/define-an-article.md).  
  
## <a name="publishing-user-defined-functions"></a>Publicar funciones definidas por el usuario  
 Las instrucciones CREATE FUNCTION para las funciones de CLR y de [!INCLUDE[tsql](../../../includes/tsql-md.md)] se copian en cada suscriptor. En el caso de las funciones CLR, también se copia el ensamblado asociado. Los cambios en las funciones se replican en los suscriptores, a diferencia de los cambios en los ensamblados asociados.  
  
## <a name="publishing-user-defined-types-and-alias-data-types"></a>Publicar tipos definidos por el usuario y tipos de datos de alias  
 Las columnas que usan tipos definidos por el usuario o tipos de datos de alias se replican en los suscriptores como cualquier otra columna. La instrucción CREATE TYPE de cada tipo replicado se ejecuta en el suscriptor antes de que se cree la tabla. En el caso de los tipos definidos por el usuario, el ensamblado asociado también se copia en cada suscriptor. Los cambios en los tipos definidos por el usuario y en los tipos de datos de alias no se replican en los suscriptores.  
  
 Si se define un tipo en una base de datos, pero no se hace referencia al mismo en ninguna columna al crear la publicación, el tipo no se copia en los suscriptores. Si posteriormente crea una columna de ese tipo en la base de datos y desea replicarla, primero debe copiar el tipo manualmente (y el ensamblado asociado de un tipo definido por el usuario) en cada suscriptor.  
  
## <a name="publishing-full-text-indexes"></a>Publicar índices de texto completo  
 La instrucción CREATE FULLTEXT INDEX se copia en cada suscriptor y el índice de texto completo se crea en el suscriptor. Los cambios realizados en los índices de texto completo con ALTER FULLTEXT INDEX no se replican.  
  
## <a name="making-schema-changes-to-published-objects"></a>Realizar cambios en el esquema de objetos publicados  
 La replicación admite una gran variedad de cambios en el esquema de objetos publicados. Cuando realice cualquiera de los siguientes cambios de esquema en el objeto publicado correspondiente en un publicador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , ese cambio se propaga de manera predeterminada a todos los suscriptores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 Para más información, vea [Realizar cambios de esquema en bases de datos de publicaciones](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md).  
  
## <a name="considerations-for-publishing"></a>Consideraciones sobre las publicaciones  
 Tenga en cuenta los siguientes aspectos a la hora de publicar objetos de base de datos:  
  
-   Los usuarios pueden tener acceso a la base de datos durante la creación de la publicación y la instantánea inicial, pero es aconsejable crear publicaciones durante los períodos de baja actividad en el publicador.  
  
-   No se puede cambiar el nombre de una base de datos después de crear en ella una publicación. Para cambiarle el nombre, primero debe quitar la replicación de la base de datos.  
  
-   Para publicar un objeto de base de datos que depende de uno o más objetos de base de datos, debe publicar todos los objetos a los que se hace referencia. Por ejemplo, si publica una vista que depende de una tabla, también debe publicar la tabla.  
  
    > [!NOTE]  
    >  Si se agrega un artículo a una publicación de combinación y ya hay un artículo que depende de este nuevo artículo, debe especificar un orden de procesamiento para los dos artículos con el parámetro **@processing_order** de [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) y [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Considere el caso siguiente: publica una tabla pero no publica una función a la que hace referencia la tabla. Si no publica la función, la tabla no se puede crear en el suscriptor. Al agregar la función a la publicación: especifique el valor **1** para el parámetro **@processing_order** de **sp_addmergearticle**y el valor **2** para el parámetro **@processing_order** de **sp_changemergearticle**; especifique el nombre de la tabla para el parámetro **@article**. Este orden de procesamiento garantiza que la función se cree en el suscriptor antes que la tabla que depende de él. Puede usar números distintos para cada artículo, siempre que el número de la función sea inferior al de la tabla.  
  
-   Los nombres de publicación no pueden incluir los caracteres siguientes: % * [ ] | : " ? \ / < >.  
  
### <a name="limitations-on-publishing-objects"></a>Limitaciones en la publicación de objetos  
  
-   El número máximo de artículos y columnas que pueden publicarse varía según el tipo de publicación. Para obtener más información, vea la sección "Replication Objects" (Objetos de replicación) de [Maximum Capacity Specifications for SQL Server](../../../sql-server/maximum-capacity-specifications-for-sql-server.md) (Especificaciones de capacidad máxima para SQL Server).  
  
-   Los procedimientos almacenados, vistas, desencadenadores y funciones definidos por el usuario que están definidos como WITH ENCRYPTION no se pueden publicar como parte de la replicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Las colecciones de esquemas XML se pueden replicar pero los cambios no se replican después de la instantánea inicial.  
  
-   Las tablas publicadas para la replicación transaccional deben tener una clave principal. Si una tabla se encuentra en una publicación de replicación transaccional, no puede deshabilitar ningún índice que esté asociado con las columnas de clave principal. Estos índices son necesarios para la replicación. Para deshabilitar un índice, primero debe quitar la tabla de la publicación.  
  
-   Los valores predeterminados enlazados creados con [sp_bindefault &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md) no se replican (los valores predeterminados enlazados ya no se usan en favor de los valores predeterminados creados con la palabra clave DEFAULT de ALTER TABLE o CREATE TABLE).  
  
-   Las funciones que contienen la sugerencia **NOEXPAND** en vistas indizadas no se pueden publicar en la misma publicación que las tablas y las vistas indizadas a las que se hace referencia, debido al orden en que el agente de distribución las entrega. Para evitar este problema, coloque la creación de tablas y vistas indizadas en una primera publicación, y agregue las funciones que contienen la sugerencia **NOEXPAND** en las vistas indizadas en una segunda publicación que se publique después de que se complete la primera publicación. O bien, cree scripts para estas funciones y entregue el script mediante el parámetro *@post_snapshot_script* de **sp_addpublication**.  
  
### <a name="schemas-and-object-ownership"></a>Esquemas y propiedad de objetos  
 La replicación tiene el siguiente comportamiento predeterminado en el Asistente para nueva publicación con respecto a los esquemas y a la propiedad de objetos:  
  
-   Para artículos de publicaciones de combinación con un nivel de compatibilidad de 90 o superior, publicaciones de instantáneas y publicaciones transaccionales: de manera predeterminada, el propietario del objeto en el suscriptor es el mismo que el propietario del objeto correspondiente en el publicador. Si en el suscriptor no existen esquemas que posean objetos, se crean de forma automática.  
  
-   Para artículos en publicaciones de combinación con un nivel de compatibilidad menor de 90: de manera predeterminada, el propietario se deja en blanco y se especifica como **dbo** durante la creación del objeto en el suscriptor.  
  
-   Para artículos de publicaciones de Oracle: de forma predeterminada, el propietario se especifica como **dbo**.  
  
-   Para artículos de publicaciones que utilizan instantáneas en modo de carácter (que se utilizan para los que no son suscriptores de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y para los suscriptores de [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ): de manera predeterminada, el propietario se deja en blanco. Como valor predeterminado del propietario se utiliza el propietario asociado con la cuenta utilizada por el Agente de distribución o el Agente de mezcla para conectarse con el suscriptor.  
  
 El propietario del objeto se puede cambiar mediante el cuadro de diálogo **Propiedades del artículo - \<***Artículo***>** y mediante los siguientes procedimientos almacenados: **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle** y **sp_changemergearticle**. Para más información, vea [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md), [Definir un artículo](../../../relational-databases/replication/publish/define-an-article.md) y [Ver y modificar las propiedades de un artículo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
### <a name="publishing-data-to-subscribers-running-previous-versions-of-sql-server"></a>Publicar datos en suscriptores que se ejecutan en versiones anteriores de SQL Server  
  
-   Si va a publicar en un suscriptor que se ejecuta en una versión anterior de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], está limitado por la funcionalidad de esa versión, tanto en cuestiones de funcionalidad específica de la replicación como en la funcionalidad general del producto.  
  
-   Las publicaciones de combinación utilizan un nivel de compatibilidad que determina las características que se pueden usar en una publicación y le permite admitir suscriptores que se ejecuten en versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
### <a name="publishing-tables-in-more-than-one-publication"></a>Publicar tablas en más de una publicación  
 La replicación es compatible con la publicación de artículos en varias publicaciones (incluso permiten volver a publicar datos) con las siguientes restricciones:  
  
-   Si un artículo se publica en una publicación transaccional y en una publicación de combinación, asegúrese de que la propiedad *@published_in_tran_pub* está establecida en TRUE para el artículo de mezcla. Para obtener más información, vea [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md) y [Ver y modificar las propiedades de un artículo](../../../relational-databases/replication/publish/view-and-modify-article-properties.md).  
  
     También debería establecer la propiedad *@published_in_tran_pub* si un artículo forma parte de una suscripción transaccional y está incluido en una publicación de combinación. Si éste es el caso, tenga en cuenta que, de forma predeterminada, la replicación transaccional espera que las tablas del suscriptor se traten como de solo lectura; si la replicación de mezcla realiza cambios en los datos de una tabla de una suscripción transaccional, se puede producir la no convergencia de los datos. Para evitar esta posibilidad, se recomienda que cada tabla de este tipo se especifique como solo para descarga en la publicación de combinación. Esto evita que un suscriptor de mezcla cargue cambios de datos en la tabla. Para obtener más información, vea [Optimizar el rendimiento de la replicación de mezcla con artículos de solo descarga](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   No es posible publicar un artículo en una publicación de combinación y en una publicación transaccional con suscripciones de actualización en cola.  
  
-   Los artículos incluidos en las publicaciones transaccionales que admiten suscripciones de actualización no se pueden volver a publicar.  
  
-   Si un artículo se publica en más de una publicación transaccional que admita suscripciones de actualización en cola, las siguientes propiedades deben tener el mismo valor para el artículo en todas las publicaciones:  
  
    |Propiedad|Parámetro en sp_addarticle|  
    |--------------|---------------------------------|  
    |Administración del intervalo de identidad|**@auto_identity_range** (en desuso) y **@identityrangemangementoption**|  
    |Intervalo de identidad del publicador|**@pub_identity_range**|  
    |Intervalo de identidad|**@identity_range**|  
    |Umbral del intervalo de identidad|**@threshold**|  
  
     Para obtener más información sobre estos parámetros, vea [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).  
  
-   Si un artículo se publica en más de una publicación de combinación, las siguientes propiedades deben tener el mismo valor para el artículo en todas las publicaciones:  
  
    |Propiedad|Parámetro en sp_addmergearticle|  
    |--------------|--------------------------------------|  
    |Seguimiento de columnas|**@column_tracking**|  
    |Opciones del esquema|**@schema_option**|  
    |Filtros de columnas|**@vertical_partition**|  
    |Opciones de carga de suscriptor|**@subscriber_upload_options**|  
    |Seguimiento condicional de eliminaciones|**@delete_tracking**|  
    |Compensación de errores|**@compensate_for_errors**|  
    |Administración del intervalo de identidad|**@auto_identity_range** (en desuso) y **@identityrangemangementoption**|  
    |Intervalo de identidad del publicador|**@pub_identity_range**|  
    |Intervalo de identidad|**@identity_range**|  
    |Umbral del intervalo de identidad|**@threshold**|  
    |Opciones de partición|**@partition_options**|  
    |Secuencias de columnas de tipo Blob|**@stream_blob_columns**|  
    |Tipo de filtro|**@filter_type** (parámetro de **sp_addmergefilter**)|  
  
     Para obtener más información sobre estos parámetros, vea [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) y [sp_addmergefilter &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md).  
  
-   La replicación transaccional y la replicación de mezcla sin filtrar admiten la publicación de una tabla en varias publicaciones y la posterior suscripción en una única tabla en la base de datos de suscripciones (es lo que normalmente se denomina un escenario de acumulación). Este tipo de escenario se suele utilizar para agregar subconjuntos de datos de varias ubicaciones en una tabla en un suscriptor central. Las publicaciones de combinación filtradas no admiten el escenario de suscriptor central. En la replicación de mezcla, la acumulación se suele implementar a través de una única publicación con filtros de fila con parámetros. Para obtener más información, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
## <a name="see-also"></a>Ver también  
 [Agregar y quitar artículos de publicaciones existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [Configurar la distribución](../../../relational-databases/replication/configure-distribution.md)   
 [Initialize a Subscription](../../../relational-databases/replication/initialize-a-subscription.md)  (Inicializar una suscripción)  
 [Crear script para la replicación](../../../relational-databases/replication/scripting-replication.md)   
 [Proteger el publicador](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [Suscribirse a publicaciones](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
