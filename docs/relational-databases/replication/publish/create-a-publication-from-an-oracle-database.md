---
title: "Crear una publicaci&#243;n a partir de una base de datos de Oracle | Microsoft Docs"
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
  - "publicaciones [replicación de SQL Server], bases de datos de Oracle"
  - "publicación de Oracle [replicación de SQL Server], configurar"
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Crear una publicaci&#243;n a partir de una base de datos de Oracle
  En este tema se describe cómo crear una publicación a partir de una base de datos de Oracle en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
-   **Para crear una publicación a partir de una base de datos de Oracle con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Antes de crear una publicación, debe instalar el software de Oracle en el distribuidor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y configurar la base de datos de Oracle. Para obtener más información, consulte [configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Cree una publicación de instantáneas o transaccional a partir de una base de datos de Oracle con el Asistente para nueva publicación.  
  
 La primera vez que cree una publicación a partir de una base de datos de Oracle, deberá identificar el publicador de Oracle en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (esto no es necesario para las publicaciones posteriores de la misma base de datos). Identificar el publicador de Oracle puede realizarse desde el Asistente para nueva publicación o **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo; en este tema se muestra el **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo.  
  
#### Para identificar el publicador de Oracle en el distribuidor de SQL Server  
  
1.  En [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que utilizará el publicador de Oracle como distribuidor y, a continuación, expanda el nodo de servidor.  
  
2.  Haga clic en el **replicación** carpeta y, a continuación, haga clic en **Propiedades del distribuidor**.  
  
3.  En el **publicadores** página de la **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo, haga clic en **Agregar**, y, a continuación, haga clic en **Agregar publicador de Oracle**.  
  
4.  En el cuadro de diálogo **Conectar al servidor** , haga clic en el botón **Opciones** .  
  
5.  En la pestaña **Inicio de sesión** :  
  
    1.  Escriba el nombre de la instancia de la base de datos de Oracle o seleccione **Buscar más** en el cuadro combinado **Instancia del servidor** .  
  
    2.  Seleccione **autenticación estándar de Oracle** (recomendado) o **autenticación de Windows**.  
  
         Si selecciona **autenticación de Windows**: el servidor de Oracle debe configurarse para permitir conexiones mediante credenciales de Windows (para obtener más información, vea la documentación de Oracle) y debe haber iniciado una sesión con la misma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] cuenta de Windows especificada para el esquema de usuario administrativo de replicación.  
  
    3.  Si selecciona **Autenticación estándar de Oracle**, escriba el nombre de inicio de sesión y la contraseña del esquema de usuario administrativo de la replicación que creó en el publicador de Oracle durante la configuración.  
  
6.  En la pestaña **Propiedades de conexión** , seleccione como tipo de publicador **Puerta de enlace** o **Completo**.  
  
     La opción **Completo** está diseñada para proporcionar publicaciones de instantáneas y transaccionales con todas las características compatibles con la publicación de Oracle. Por su parte, la opción **Puerta de enlace** proporciona optimizaciones de diseño específicas para mejorar el rendimiento en casos en los que la replicación sirva como puerta de enlace entre sistemas. La opción **Puerta de enlace** no se puede utilizar si tiene previsto publicar la misma tabla en varias publicaciones transaccionales. Una tabla puede aparecer como máximo en una publicación transaccional y en cualquier número de publicaciones de instantáneas si selecciona **Puerta de enlace**.  
  
7.  Haga clic en **Conectar**para crear una conexión al publicador de Oracle y configurarla para la replicación. El **Conectar con el servidor** cuadro de diálogo se cierra y se devuelven a la **Propiedades del distribuidor: \< distribuidor>** cuadro de diálogo.  
  
    > [!NOTE]  
    >  En este punto, si hay algún problema con la configuración de la red, recibirá un error. Si tiene problemas para conectarse a la base de datos de Oracle, vea la sección en la que se explica qué hacer cuando el distribuidor de SQL Server no puede conectarse a la base de datos de Oracle, en el tema [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para crear una publicación a partir de una base de datos de Oracle  
  
1.  Conéctese a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que el publicador de Oracle utilizará como distribuidor y, a continuación, expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** .  
  
3.  Haga clic en el **publicaciones locales** carpeta y, a continuación, haga clic en **nueva publicación de Oracle**.  
  
4.  En la página **Publicador de Oracle** del Asistente para nueva publicación, seleccione el publicador de Oracle. Si no aparece el publicador de Oracle, haga clic en **Agregar publicador de Oracle**, que le guiará por los pasos del procedimiento anterior.  
  
5.  En la página **Tipo de publicación** , seleccione **Publicación de instantáneas** o **Publicación transaccional**.  
  
6.  En la página **Artículos** , seleccione los objetos de base de datos que desea publicar.  
  
     Si lo desea, filtre las columnas de la tabla; para ello, expanda una tabla y desactive la casilla de una o varias columnas. Haga clic en **Propiedades del artículo** para ver y modificar las propiedades del artículo, y especificar otras asignaciones de tipos de datos, si es necesario. Para obtener más información acerca de las asignaciones de tipo de datos, consulte [especificar asignaciones de tipos de datos de un publicador de Oracle](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md).  
  
7.  De forma opcional, en la página **Filtrar filas de tabla** , aplique filtros para publicar un subconjunto de datos de una o más tablas.  
  
8.  En la página **Agente de instantáneas** , desactive la casilla **Crear una instantánea inmediatamente** solo si ya ha creado todos los objetos y ha agregado todos los datos necesarios a la base de datos de suscripciones.  
  
9. En la **seguridad del agente** página, especifique las credenciales para el agente de instantáneas (para todas las publicaciones) y el agente de lector del registro (para las publicaciones transaccionales). Los agentes se ejecutarán y establecerán conexiones con el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando el contexto de la cuenta de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows especificada. Los agentes establecerán conexiones con la base de datos de Oracle utilizando el contexto de la cuenta especificada como esquema de usuario administrativo de la replicación. Para obtener más información, consulte [configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
     Para obtener más información acerca de los permisos que necesita cada agente, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) y [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
10. En la página **Acciones** del Asistente, puede crear un script para la publicación. Para obtener más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
11. En la página **Finalización del asistente** , especifique el nombre de la publicación.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Una vez configurada como publicador la base de datos de Oracle, puede crear una publicación transaccional o de instantáneas del mismo modo en que lo haría desde un publicador de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , mediante procedimientos almacenados del sistema.  
  
#### Para crear una publicación Oracle  
  
1.  Configure la base de datos Oracle como publicador. Para obtener más información, consulte [configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
2.  Si no existe ningún distribuidor remoto, configúrelo. Para obtener más información, consulte [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
3.  En el distribuidor remoto que utilizará el publicador de Oracle, ejecute [sp_adddistpublisher & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md). Especifique el nombre de sustrato de red transparente (TNS) de la instancia de base de datos de Oracle para **@publisher** y un valor de **ORACLE** o **puerta de enlace de ORACLE** para **@publisher_type**. `Specify` el modo de seguridad que se usa en la conexión desde el publicador de Oracle al distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] remoto como uno de los siguientes:  
  
    -   Para usar la autenticación estándar de Oracle, el valor predeterminado, especifique un valor de **0** para **@security_mode**, el inicio de sesión del esquema de usuario administrativo de replicación que creó en el publicador de Oracle durante la configuración de **@login**, y la contraseña de **@password**.  
  
        > [!IMPORTANT]  
        >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si almacena credenciales en un archivo de script, debe proteger el archivo para evitar el acceso no autorizado.  
  
    -   Para utilizar la autenticación de Windows, especifique un valor de **1** para **@security_mode**.  
  
        > [!NOTE]  
        >  Para usar autenticación de Windows, el servidor de Oracle debe estar configurado para admitir conexiones con credenciales de Windows (para obtener más información, vea la documentación de Oracle) y deberá haber iniciado una sesión con la misma cuenta de Microsoft Windows que especificó para el esquema de usuario administrativo de replicación.  
  
4.  Cree un trabajo de Agente de registro del LOG para la base de datos de publicación.  
  
    -   Si no está seguro de si existe un trabajo del agente de lector del registro para una base de datos publicada, ejecute [sp_helplogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) en el distribuidor utilizado por el publicador de Oracle en la base de datos de distribución. Especifique el nombre del publicador de Oracle en **@publisher**. Si el conjunto de resultados está vacío, es necesario crear un trabajo de Agente de registro del LOG.  
  
    -   Si ya existe un trabajo de Agente de registro del LOG para la base de datos de publicación, continúe en el paso 5.  
  
    -   En el distribuidor utilizado por el publicador de Oracle en la base de datos de distribución, ejecute [sp_addlogreader_agent & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique las credenciales de Windows en la que se ejecuta el agente de **@job_login** y **@job_password**.  
  
        > [!NOTE]  
        >  El **@job_login** parámetro debe coincidir con el inicio de sesión proporcionado en el paso 3. No proporcione información de seguridad del editor. El Agente de registro del LOG se conecta al publicador utilizando la información de seguridad proporcionada en el paso 3.  
  
5.  En el distribuidor en la base de datos de distribución, ejecute [sp_addpublication & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) Para crear la publicación. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  En el distribuidor en la base de datos de distribución, ejecute [sp_addpublication_snapshot & #40; Transact-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique el nombre de publicación usado en el paso 4 para **@publication** y las credenciales de Windows en la que se ejecuta el agente de instantáneas para **@job_name** y **@password**. Para usar la autenticación estándar de Oracle al conectarse al publicador, también debe especificar un valor de **0** para **@publisher_security_mode** y la información de inicio de sesión de Oracle para **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
## Vea también  
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Configurar el trabajo de conjunto de transacciones para un publicador de Oracle & #40; Programación de replicación Transact-SQL & #41;](../../../relational-databases/replication/administration/configure the transaction set job for an oracle publisher.md)   
 [Información general de la publicación de Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [Script para conceder permisos en Oracle](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  