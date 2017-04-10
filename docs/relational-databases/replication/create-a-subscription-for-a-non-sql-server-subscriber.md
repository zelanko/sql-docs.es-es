---
title: "Crear una suscripci&#243;n para un suscriptor que no sea de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "suscripciones [replicación de SQL Server], suscriptores que no son de SQL Server"
  - "suscriptores [replicación de SQL Server], suscriptores que no son de SQL Server"
  - "suscriptores que no son de SQL Server, suscripciones"
ms.assetid: 5020ee68-b988-4d57-8066-67d183e61237
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# Crear una suscripci&#243;n para un suscriptor que no sea de SQL Server
  En este tema se describe cómo crear una suscripción para un suscriptor que no sea de SQL Server en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. La replicación transaccional y la replicación de instantáneas admiten la publicación de datos en suscriptores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información acerca de las plataformas admitidas de suscriptor, consulte [suscriptores no SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
 **En este tema**  
  
-   **Para crear una suscripción para un suscriptor que no sea de SQL Server con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Para crear una publicación para un suscriptor que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
1.  Instale y configure el software de cliente y el proveedor o proveedores OLE DB adecuados en el distribuidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) y [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
2.  Cree una publicación mediante el Asistente para nueva publicación. Para obtener más información sobre la creación de publicaciones, vea [crear una publicación](../../relational-databases/replication/publish/create-a-publication.md) y [crear una publicación de una base de datos de Oracle](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md). En el Asistente para nueva publicación, especifique las siguientes opciones:  
  
    -   En la página **Tipo de publicación** , seleccione **Publicación de instantáneas** o **Publicación transaccional**.  
  
    -   En la página **Agente de instantáneas** , desactive **Crear una instantánea inmediatamente**.  
  
         La instantánea se crea una vez habilitada la publicación para los suscriptores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fin de garantizar que el Agente de instantáneas genera scripts de inicialización e instantáneas adecuados para los suscriptores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
3.  Habilitar la publicación no es[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los suscriptores utilizan la **Propiedades de publicación: \< Nombredepublicación>** cuadro de diálogo. Para obtener más información acerca de este paso, vea [Publication Properties, Subscription Options](../../relational-databases/replication/publication-properties-subscription-options.md) .  
  
4.  Cree una suscripción mediante el Asistente para nuevas suscripciones. En este tema se proporciona más información acerca de este paso.  
  
5.  (Opcional) Cambiar el **pre_creation_cmd** propiedad para conservar las tablas del suscriptor del artículo. En este tema se proporciona más información acerca de este paso.  
  
6.  Genere una instantánea para la publicación. En este tema se proporciona más información acerca de este paso.  
  
7.  Sincronice la suscripción. Para más información, consulte [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md).  
  
#### Para habilitar una publicación para suscriptores que no son de SQL Server  
  
1.  Conéctese al publicador en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo del servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic en la publicación y, a continuación, haga clic en **propiedades**.  
  
4.  En el **Opciones de suscripción** seleccione un valor de **True** para la opción **Permitir suscriptores que no sean de SQL Server**. Al seleccionar esta opción, se modifican una serie de propiedades para que la publicación sea compatible con suscriptores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    > [!NOTE]  
    >  Seleccionar **True** establece el valor de la **pre_creation_cmd** 'drop' a la propiedad del artículo. El valor mencionado indica que la replicación debe quitar una tabla en el suscriptor si coincide con el nombre de la tabla del artículo. Si tiene tablas existentes en el suscriptor que desea conservar, use la [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) del procedimiento almacenado para cada artículo; Especifique un valor 'none' para **pre_creation_cmd**: `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] Se le pedirá que cree una nueva instantánea para la publicación. Si no desea crear ninguna en este momento, siga los pasos descritos en el procedimiento correspondiente más adelante.  
  
#### Para crear una suscripción para un suscriptor que no sea de SQL Server  
  
1.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
2.  Haga clic en la publicación apropiada y, a continuación, haga clic en **nuevas suscripciones**.  
  
3.  En la página **Ubicación del Agente de distribución** , asegúrese de que la opción **Ejecutar todos los agentes en el distribuidor** está seleccionada. Los suscriptores que no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no pueden ejecutar agentes en el suscriptor.  
  
4.  En el **suscriptores** haga clic en **Agregar suscriptor** y, a continuación, haga clic en **Agregar suscriptor que no son de SQL Server**.  
  
5.  En el **Agregar suscriptor que no son de SQL Server** cuadro de diálogo, seleccione el tipo de suscriptor.  
  
6.  Especifique un valor en **Nombre del origen de datos**:  
  
    -   Para Oracle, es el nombre TNS (transparent network substrate) configurado.  
  
    -   Para IBM, puede ser cualquier nombre. Lo habitual es especificar la dirección de red del suscriptor.  
  
     El asistente no valida el nombre del origen de datos especificado en este paso ni las credenciales del paso 9. No se utilizan para la replicación hasta que se ejecuta el Agente de distribución para la suscripción. Asegúrese de que todos los valores se han probado conectándose al suscriptor mediante una herramienta cliente (como **sqlplus** para Oracle). Para obtener más información, consulte [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) y [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] En el **suscriptores** página del asistente, el suscriptor se muestra ahora en el **suscriptor** columna de sólo lectura **(destino predeterminado)** en el **base de datos de suscripción** columna:  
  
    -   En Oracle, un servidor tiene como máximo una base de datos, por lo que no es necesario especificarla.  
  
    -   Para IBM DB2, la base de datos se especifica en la propiedad **Catálogo inicial** de la cadena de conexión DB2, la cual puede indicarse en el campo **Opciones de conexión adicionales** que se describe más adelante en este proceso.  
  
8.  En la **seguridad del agente de distribución** haga clic en el botón de propiedades (**...**) situado junto al suscriptor para obtener acceso a la **seguridad del agente de distribución** cuadro de diálogo.  
  
9. En el cuadro de diálogo **Seguridad del Agente de distribución** :  
  
    -   En los campos **Cuenta de proceso**, **Contraseña**y **Confirmar contraseña** , especifique la cuenta y contraseña de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con las que se deberá ejecutar el Agente de distribución y establecer las conexiones locales al distribuidor.  
  
         La cuenta requiere los siguientes permisos mínimos: miembro de la **db_owner** fija rol de base de datos en la base de datos de distribución, los miembros de la lista de acceso de la publicación (PAL); permisos de lectura en el recurso compartido de instantáneas y permiso de lectura en el directorio de instalación del proveedor OLE DB. Para obtener más información acerca de la PAL, consulte [proteger el publicador](../../relational-databases/replication/security/secure-the-publisher.md).  
  
    -   En **Conectar al suscriptor**, en los campos **Inicio de sesión**, **Contraseña**y **Confirmar contraseña** , escriba el nombre de inicio de sesión y la contraseña que deben utilizarse para conectar al suscriptor. Este inicio de sesión ya debería estar configurado y disponer de los permisos suficientes para crear objetos en la base de datos de suscripciones.  
  
    -   En el **Opciones de conexión adicionales** especifique las opciones de conexión para el suscriptor en forma de una cadena de conexión (Oracle no requiere opciones adicionales). Las opciones deben ir separadas con punto y coma. A continuación se ofrece un ejemplo de una cadena de conexión DB2 (se han incluido saltos de línea para facilitar la lectura):  
  
        ```  
        Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
        PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
        Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
        Persist Security Info=False;Connection Pooling=True;  
        ```  
  
         La mayoría de las opciones de la cadena son específicas para el servidor DB2 que está configurando, pero la opción **Process Binary as Character** siempre debe establecerse en **False**. Se requiere un valor para que la opción **Catálogo original** identifique la base de datos de suscripciones.  
  
10. En el **programación de sincronización** seleccione una programación para el agente de distribución desde el **programación del agente** menú (suele ser la programación **se ejecutan continuamente**).  
  
11. En la página **Inicializar suscripciones** , especifique si la suscripción debe inicializarse y, en ese caso, cuándo debe llevarse a cabo:  
  
    -   Desactive **Inicializar** únicamente si ha creado todos los objetos y agregado todos los datos necesarios a la base de datos de suscripciones.  
  
    -   Seleccione **inmediatamente** en la lista desplegable de la **inicializar cuando** columna tengan la transferencia del agente de distribución archivos de instantánea al suscriptor una vez finalizado el asistente. Seleccione **En la primera sincronización** para que el agente transfiera los archivos la próxima vez que esté programado para ejecutarse.  
  
12. En la página **Acciones del asistente** , incluya de forma opcional la suscripción. Para obtener más información, consulte [Scripting Replication](../../relational-databases/replication/scripting-replication.md).  
  
#### Para conservar las tablas en el suscriptor  
  
-   De forma predeterminada, al habilitar una publicación para no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suscriptores establece el valor de la **pre_creation_cmd** 'drop' a la propiedad del artículo. El valor mencionado indica que la replicación debe quitar una tabla en el suscriptor si coincide con el nombre de la tabla del artículo. Si tiene tablas existentes en el suscriptor que desea conservar, use la [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) del procedimiento almacenado para cada artículo; Especifique un valor 'none' para **pre_creation_cmd**. `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`.  
  
#### Para generar una instantánea para la publicación  
  
1.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
2.  Haga clic en la publicación y, a continuación, haga clic en **Ver estado del agente de instantáneas**.  
  
3.  En el **Ver estado del agente de instantáneas - \< publicación>** cuadro de diálogo, haga clic en **iniciar**.  
  
 Cuando el Agente de instantáneas termina de generar la instantánea, aparece un mensaje del tipo "[100%] Se ha generado una instantánea de 17 artículos".  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Puede crear suscripciones de inserción para suscriptores que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante programación con procedimientos almacenados de replicación.  
  
> [!IMPORTANT]  
>  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
#### Para crear una suscripción de inserción para una publicación transaccional o de instantáneas a un suscriptor que no sea de SQL Server  
  
1.  Instale el proveedor OLE DB más reciente para el Suscriptor que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el Publicador y el Distribuidor. Para los requisitos de replicación para un proveedor OLE DB, vea [suscriptores no SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md), [suscriptores de Oracle](../../relational-databases/replication/non-sql/oracle-subscribers.md), [suscriptores de IBM DB2](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
2.  En el publicador de la base de datos de publicación, compruebe que la publicación admite no[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suscriptores ejecutando [sp_helppublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md).  
  
    -   Si el valor de **enabled_for_het_sub** es 1, no es[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se admiten los suscriptores.  
  
    -   Si el valor de **enabled_for_het_sub** es 0, ejecutar [sp_changepublication & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), especificando **enabled_for_het_sub** para **@property** y **true** para **@value**.  
  
        > [!NOTE]  
        >  Antes de cambiar **enabled_for_het_sub** a **true**, debe quitar las suscripciones existentes a la publicación. No se puede establecer **enabled_for_het_sub** a **true** cuando la publicación también admite suscripciones de actualización. Cambiar **enabled_for_het_sub** afectará a otras propiedades de la publicación. Para obtener más información, consulte [suscriptores no SQL Server](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md).  
  
3.  En el publicador de la base de datos de publicación, ejecute [sp_addsubscription & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md). Especifique **@publication**, **@subscriber**, un valor de **(destino predeterminado)** de **@destination_db**, un valor de **inserción** para **@subscription_type**, y un valor de 3 para **@subscriber_type** (especifica un proveedor OLE DB).  
  
4.  En el publicador de la base de datos de publicación, ejecute [sp_addpushsubscription_agent & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md). Especifique lo siguiente:  
  
    -   Los parámetros **@subscriber**y **@publication** .  
  
    -   Un valor de **(destino predeterminado)** para **@subscriber_db**,  
  
    -   Las propiedades de no es[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de origen de datos para **@subscriber_provider**, **@subscriber_datasrc**, **@subscriber_location**, **@subscriber_provider_string**, y **@subscriber_catalog**.  
  
    -   El [!INCLUDE[msCoName](../../includes/msconame-md.md)] las credenciales de Windows bajo la que se ejecuta el agente de distribución en el distribuidor para **@job_login** y **@job_password**.  
  
        > [!NOTE]  
        >  Las conexiones realizadas mediante la autenticación integrada de Windows siempre utilizan las credenciales de Windows especificadas por **@job_login** y **@job_password**. El Agente de distribución siempre realiza la conexión local con el distribuidor mediante la autenticación integrada de Windows. De forma predeterminada, el agente se conectará con el suscriptor mediante la autenticación integrada de Windows.  
  
    -   Un valor de **0** para **@subscriber_security_mode** y la información de inicio de sesión del proveedor OLE DB para **@subscriber_login** y **@subscriber_password**.  
  
    -   Una programación para el trabajo del Agente de distribución de esta suscripción. Para obtener más información, consulte [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md).  
  
    > [!IMPORTANT]  
    >  Al crear una suscripción de inserción en un publicador con un distribuidor remoto, los valores suministrados para todos los parámetros, incluidos *job_login* y *job_password*, se envían al distribuidor como texto sin formato. Antes de ejecutar este procedimiento almacenado, se recomienda cifrar la conexión entre el publicador y su distribuidor remoto. Para obtener más información, consulte [Habilitar conexiones cifradas en el motor de base de datos & #40; SQL Server Configuration Manager y nº 41;](../../database-engine/configure-windows/enable encrypted connections to the database engine.md).  
  
## Vea también  
 [suscriptores de IBM DB2](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Suscriptores de Oracle](../../relational-databases/replication/non-sql/oracle-subscribers.md)   
 [Otros suscriptores que no son de SQL Server](../../relational-databases/replication/non-sql/other-non-sql-server-subscribers.md)   
 [Conceptos sobre los procedimientos almacenados del sistema de replicación](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Prácticas recomendadas de seguridad de replicación](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  