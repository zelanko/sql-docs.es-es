---
title: "Administrar columnas de identidad | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "valores de identidad [replicación de SQL Server]"
  - "replicación de mezcla [replicación de SQL Server], administración de intervalos de identidad"
  - "publicar [replicación de SQL Server], columnas de identidad"
  - "replicación transaccional, administración de intervalos de identidad"
  - "columnas de identidad [SQL Server], replicación"
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# Administrar columnas de identidad
  En este tema se describe cómo administrar columnas de identidad en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Cuando las inserciones del Suscriptor se replican de nuevo al Publicador, se deben administrar las columnas de identidad para evitar la asignación del mismo valor de identidad en el Suscriptor y el Publicador. La replicación puede administrar automáticamente intervalos de identidad o puede elegir procesar manualmente la administración de intervalos de identidad.  Para obtener información acerca de las opciones de administración de intervalos de identidad proporcionadas por la replicación, consulte [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
-   **Para administrar columnas de identidad con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Al publicar una tabla en más de una publicación, debe especificar las mismas opciones de administración de intervalos de identidad para ambas publicaciones. Para obtener más información, consulte "Publicación tablas en varias publicaciones" en [publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md).  
  
-   Para crear un número se incrementa automáticamente que se puede utilizar en varias tablas o que se puede llamar desde las aplicaciones sin hacer referencia a cualquier tabla, consulte [números de secuencia](../../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especificar una opción de administración de la columna de identidad en la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo del Asistente para nueva publicación. Para obtener más información acerca de cómo utilizar este asistente, consulte [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md). En el Asistente para nueva publicación:  
  
-   Si selecciona **publicación de mezcla** o **una publicación transaccional con suscripciones actualizables** en el **tipo de publicación** seleccione Administración de intervalos de identidad automático o manual (automático, el valor predeterminado, se recomienda). Una vez publicada la tabla, la propiedad no se puede modificar, pero otras propiedades relacionadas sí se pueden modificar.  
  
-   Si selecciona otros tipos de publicaciones, debe establecer la administración de los intervalos de identidad en manual.  
  
 Modificar intervalos de identidad y los umbrales en la **propiedades** ficha de la **Propiedades del artículo: \< artículo>**, que está disponible en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar una opción de administración de las columnas de identidad  
  
1.  Si el publicador está ejecutando una versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anterior a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], en la página **Tipo de publicación** del Asistente para nueva publicación, seleccione **Publicación de combinación** o **Publicación transaccional con suscripciones actualizables**.  
  
2.  En la página **Artículos** , seleccione una tabla con una columna de identidad.  
  
3.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
4.  En la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo el **administración de intervalos de identidad** sección, establezca el **administrar intervalos de identidad automáticamente** propiedad **automática** o **Manual** (para publicadores que ejecutan [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior), o **True** o **False** (para publicadores que ejecutan una versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]).  
  
5.  Si seleccionó **Automático** o **True** en el paso 4, escriba los valores de las opciones en la siguiente tabla. Para obtener más información acerca de cómo utilizar estas opciones, vea la sección "Asignar intervalos de identidad" de [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
    |Opción|Valor|Descripción|  
    |------------|-----------|-----------------|  
    |**Tamaño de intervalo del publicador**|Valor entero para el tamaño del intervalo (por ejemplo, 20 000).|Consulte la sección "Asignar intervalos de identidad" de [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).|  
    |**Tamaño de intervalo del suscriptor**|Valor entero para el tamaño del intervalo (por ejemplo, 10000).|Consulte la sección "Asignar intervalos de identidad" de [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).|  
    |**Porcentaje de umbral del intervalo**|Valor entero para el umbral de porcentaje (por ejemplo, 90 equivale a 90 por ciento).|Porcentaje del total de valores de identidad utilizados en un nodo antes de que se asigne un nuevo intervalo de identidad.<br /><br /> <br /><br /> Nota: Este valor se debe especificar, pero solo lo utilizan suscriptores que usan suscripciones de actualización en cola y suscriptores de publicaciones de combinación que ejecuten [!INCLUDE[ssEW](../../../includes/ssew-md.md)] o versiones anteriores de otras ediciones de SQL Server. Para obtener más información, vea la sección "Asignar intervalos de identidad" de [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).|  
    |**Valor de inicio del siguiente intervalo**|Valor entero. Solo lectura.|El valor en el que comenzará el siguiente intervalo. Por ejemplo, si el intervalo actual es 5001-6000, este valor será 6001.|  
    |**Valor máximo de identidad**|Valor entero. Solo lectura.|El valor más grande de la columna de identidad. Está determinado por el tipo de datos base de la columna.|  
    |**Incremento**|Valor entero. Solo lectura.|La cantidad en la que se debe incrementar o reducir el número de la columna de identidad para cada inserción: por lo general se establece en 1.|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para modificar los intervalos de identidad y los umbrales una vez publicada la tabla  
  
1.  En el **artículos** página de la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione una tabla con una columna de identidad.  
  
2.  Haga clic en **Propiedades del artículo**y, a continuación, haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
3.  En la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo el **administración de intervalos de identidad** sección, especifique valores para una o varias de las siguientes propiedades: **tamaño de intervalo del publicador**, **tamaño de intervalo del suscriptor**, y **el porcentaje de umbral de intervalo**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Haga clic en **Aceptar** en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede usar los procedimientos almacenados de replicación para especificar las opciones de administración de intervalos de identidad cuando se crea un artículo.  
  
#### Para habilitar la administración automática de intervalos de identidad al definir artículos para una publicación transaccional  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Si la tabla de origen que se está publicada tiene una columna de identidad, especifique un valor de **automática** para **@identityrangemanagementoption**, el intervalo de valores de identidad asignado al publicador para **@pub_identity_range**, el intervalo de valores de identidad asignados a cada suscriptores para **@identity_range**, y el porcentaje total de valores de identidad utilizados antes de que se asigna un nuevo intervalo de identidad para **@threshold**. Para obtener más información acerca de cómo definir los artículos, vea [definir un artículo](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Asegúrese de que el tipo de datos de la columna de identidad es lo bastante grande como para admitir el intervalo total de identidades que se están asignando a todos los Suscriptores.  
  
#### Para deshabilitar la administración automática de intervalos de identidad al definir artículos para una publicación transaccional  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique un valor de **manual** para **@identityrangemanagementoption**. Para obtener más información acerca de cómo definir los artículos, vea [definir un artículo](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Asigne intervalos para identificar las columnas de artículo en el Suscriptor para evitar la generación de conflictos para actualizar los Suscriptores. Para obtener más información, vea la sección sobre cómo asignar intervalos para la administración de intervalos de identidad manual en el tema [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
#### Para habilitar la administración automática de intervalos de identidad al definir artículos para una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Si la tabla de origen que se está publicada tiene una columna de identidad, especifique un valor de **automática** para **@identityrangemanagementoption**, el intervalo de valores de identidad asignados a una suscripción de servidor para **@pub_identity_range**, el intervalo de valores de identidad asignado al publicador y a cada suscripción de cliente para **@identity_range**, y el porcentaje total de valores de identidad utilizados antes de que se asigna un nuevo intervalo de identidad para **@threshold**. Para obtener más información sobre cuándo se asignan los nuevos intervalos de identidad, vea asignar intervalos de identidad en el tema [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md). Para obtener más información acerca de cómo definir los artículos, vea [definir un artículo](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Asegúrese de que el tipo de datos de la columna de identidad es lo bastante grande como para admitir el intervalo total de identidades que se están asignando a todos los Suscriptores, particularmente para los Suscriptores con suscripciones de servidor.  
  
#### Para deshabilitar la administración automática de intervalos de identidad al definir artículos para una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique uno de los valores siguientes para **@identityrangemanagementoption**:  
  
    -   **manual** -intervalos de identidad deben asignarse manualmente para actualizar suscriptores.  
  
    -   **Ninguno** -las columnas de identidad en el publicador no se definirán como columnas de identidad en el suscriptor.  
  
     Para obtener más información acerca de cómo definir los artículos, vea [definir un artículo](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Asigne intervalos para identificar las columnas de artículo en el Suscriptor para evitar la generación de conflictos para actualizar los Suscriptores.  
  
#### Para cambiar los valores de administración automática de intervalos de identidad para un artículo existente en una publicación transaccional o de instantáneas  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md) y anote el valor de **identityrangemanagementoption** conjunto de resultados. Si este valor es **0**, la administración automática de intervalos de identidad no está habilitada.  
  
2.  Si el valor de **identityrangemanagementoption** en el conjunto de resultados es **1**, cambie la configuración de la siguiente manera:  
  
    -   Para cambiar los intervalos de identidad asignados, ejecute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **identity_range** o **pub_identity_range** para **@property** y el nuevo valor de intervalo de **@value**.  
  
    -   Para cambiar el umbral en el que los nuevos intervalos están asignados, ejecute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **threshold** para **@property** y el nuevo valor umbral para **@value**.  
  
#### Para cambiar la configuración de administración automática de intervalos de identidad para un artículo existente en una publicación de combinación  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) y anote el valor de **identity_support** conjunto de resultados. Si este valor es **0**, la administración automática de intervalos de identidad no está habilitada.  
  
2.  Si el valor de **identity_support** en el resultado es el conjunto **1**, cambie la configuración como sigue:  
  
    -   Para cambiar los intervalos de identidad asignados, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **identity_range** o **pub_identity_range** para **@property** y el nuevo valor de intervalo de **@value**.  
  
    -   Para cambiar el umbral en el que los nuevos intervalos están asignados, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **threshold** para **@property** y el nuevo valor umbral para **@value**. Para obtener más información sobre cuándo se asignan los nuevos intervalos de identidad, vea asignar intervalos de identidad en el tema [replicar las columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md).  
  
    -   Para deshabilitar la administración del intervalo automático de identidad, ejecute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) en el publicador de la base de datos de publicación. Especifique un valor de **identityrangemanagementoption** para **@property** y **manual** o **ninguno** para **@value**.  
  
## Vea también  
 [Replicación transaccional punto a punto](../../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Replicar columnas de identidad](../../../relational-databases/replication/publish/replicate-identity-columns.md)  
  
  