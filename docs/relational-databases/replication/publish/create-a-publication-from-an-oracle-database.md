---
title: Creación de una publicación a partir de una base de datos de Oracle | Microsoft Docs
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
- publications [SQL Server replication], Oracle databases
- Oracle publishing [SQL Server replication], configuring
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f8f8aba1972cae5e92be6ea9456c836986af8514
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-publication-from-an-oracle-database"></a>Crear una publicación a partir de una base de datos de Oracle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describe cómo crear una publicación a partir de una base de datos de Oracle en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Requisitos previos](#Prerequisites)  
  
-   **Para crear una publicación a partir de una base de datos de Oracle con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Antes de crear una publicación, debe instalar el software de Oracle en el distribuidor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y configurar la base de datos de Oracle. Para obtener más información, vea [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Cree una publicación de instantáneas o transaccional a partir de una base de datos de Oracle con el Asistente para nueva publicación.  
  
 La primera vez que cree una publicación a partir de una base de datos de Oracle, deberá identificar el publicador de Oracle en el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (esto no es necesario para las publicaciones posteriores de la misma base de datos). Puede identificar el publicador de Oracle desde el Asistente para nueva publicación o el cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>**. En este tema se muestra el cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>**.  
  
#### <a name="to-identify-the-oracle-publisher-at-the-sql-server-distributor"></a>Para identificar el publicador de Oracle en el distribuidor de SQL Server  
  
1.  En [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que utilizará el publicador de Oracle como distribuidor y, a continuación, expanda el nodo de servidor.  
  
2.  Haga clic con el botón secundario en la carpeta **Replicación** y, a continuación, haga clic en **Propiedades del distribuidor**.  
  
3.  En la página **Publicadores** del cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>**, haga clic en **Agregar** y, después, en **Agregar publicador de Oracle**.  
  
4.  En el cuadro de diálogo **Conectar al servidor** , haga clic en el botón **Opciones** .  
  
5.  En la pestaña **Inicio de sesión** :  
  
    1.  Escriba el nombre de la instancia de la base de datos de Oracle o seleccione **Buscar más** en el cuadro combinado **Instancia del servidor** .  
  
    2.  Seleccione **Autenticación estándar de Oracle** (opción recomendada) o **Autenticación de Windows**.  
  
         Si selecciona **Autenticación de Windows**: deberá configurar el servidor de Oracle para que admita conexiones con credenciales de Windows (para obtener más información, vea la documentación de Oracle) y deberá haber iniciado una sesión con la misma cuenta de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows que especificó para el esquema de usuario administrativo de la replicación.  
  
    3.  Si selecciona **Autenticación estándar de Oracle**, escriba el nombre de inicio de sesión y la contraseña del esquema de usuario administrativo de la replicación que creó en el publicador de Oracle durante la configuración.  
  
6.  En la pestaña **Propiedades de conexión** , seleccione como tipo de publicador **Puerta de enlace** o **Completo**.  
  
     La opción **Completo** está diseñada para proporcionar publicaciones de instantáneas y transaccionales con todas las características compatibles con la publicación de Oracle. La opción **Puerta de enlace** proporciona optimizaciones de diseño específicas para mejorar el rendimiento en casos en los que la replicación sirva como puerta de enlace entre sistemas. La opción **Puerta de enlace** no se puede utilizar si tiene previsto publicar la misma tabla en varias publicaciones transaccionales. Una tabla puede aparecer como máximo en una publicación transaccional y en cualquier número de publicaciones de instantáneas si selecciona **Puerta de enlace**.  
  
7.  Haga clic en **Conectar**para crear una conexión al publicador de Oracle y configurarla para la replicación. Se cerrará el cuadro de diálogo **Conectar con el servidor** y volverá al cuadro de diálogo **Propiedades del distribuidor - \<distribuidor>**.  
  
    > [!NOTE]  
    >  En este punto, si hay algún problema con la configuración de la red, recibirá un error. Si tiene problemas para conectarse a la base de datos de Oracle, vea la sección en la que se explica qué hacer cuando el distribuidor de SQL Server no puede conectarse a la base de datos de Oracle, en el tema [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md).  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-create-a-publication-from-an-oracle-database"></a>Para crear una publicación a partir de una base de datos de Oracle  
  
1.  Conéctese a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que el publicador de Oracle utilizará como distribuidor y, a continuación, expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** .  
  
3.  Haga clic con el botón secundario en la carpeta **Publicaciones locales** y, a continuación, elija **Nueva publicación de Oracle**.  
  
4.  En la página **Publicador de Oracle** del Asistente para nueva publicación, seleccione el publicador de Oracle. Si no aparece el publicador de Oracle, haga clic en **Agregar publicador de Oracle**, que le guiará por los pasos del procedimiento anterior.  
  
5.  En la página **Tipo de publicación** , seleccione **Publicación de instantáneas** o **Publicación transaccional**.  
  
6.  En la página **Artículos** , seleccione los objetos de base de datos que desea publicar.  
  
     Si lo desea, filtre las columnas de la tabla; para ello, expanda una tabla y desactive la casilla de una o varias columnas. Haga clic en **Propiedades del artículo** para ver y modificar las propiedades del artículo, y especificar otras asignaciones de tipos de datos, si es necesario. Para especificar asignaciones de datos alternativas, vea [Especificar asignaciones de tipos de datos para un publicador de Oracle](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md).  
  
7.  De forma opcional, en la página **Filtrar filas de tabla** , aplique filtros para publicar un subconjunto de datos de una o más tablas.  
  
8.  En la página **Agente de instantáneas** , desactive la casilla **Crear una instantánea inmediatamente** solo si ya ha creado todos los objetos y ha agregado todos los datos necesarios a la base de datos de suscripciones.  
  
9. En la página **Seguridad del agente** , especifique las credenciales para el Agente de instantáneas (para todas las publicaciones) y el Agente de registro del LOG (para las publicaciones transaccionales). Los agentes se ejecutarán y establecerán conexiones con el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizando el contexto de la cuenta de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows especificada. Los agentes establecerán conexiones con la base de datos de Oracle utilizando el contexto de la cuenta especificada como esquema de usuario administrativo de la replicación. Para obtener más información, vea [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
     Para obtener más información acerca de los permisos que necesita cada agente, vea [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) y [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
10. En la página **Acciones** del Asistente, puede crear un script para la publicación. Para obtener más información, consulte [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
11. En la página **Finalización del asistente** , especifique el nombre de la publicación.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Una vez configurada como publicador la base de datos de Oracle, puede crear una publicación transaccional o de instantáneas del mismo modo en que lo haría desde un publicador de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , mediante procedimientos almacenados del sistema.  
  
#### <a name="to-create-an-oracle-publication"></a>Para crear una publicación Oracle  
  
1.  Configure la base de datos Oracle como publicador. Para obtener más información, vea [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
2.  Si no existe ningún distribuidor remoto, configúrelo. Para obtener más información, consulte [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md).  
  
3.  En el distribuidor remoto que utilizará el publicador de Oracle, ejecute [sp_adddistpublisher &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md). Especifique el nombre TNS (Transparent Network Substrate, Sustrato de red transparente) de la instancia de base de datos de Oracle para **@publisher** y un valor de **ORACLE** o **ORACLE GATEWAY** para **@publisher_type**. `Specify` el modo de seguridad que se usa en la conexión desde el publicador de Oracle al distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] remoto como uno de los siguientes:  
  
    -   Para utilizar autenticación estándar de Oracle, el valor predeterminado, especifique el valor **0** para **@security_mode**, el inicio de sesión del esquema de usuario administrativo de replicación que creó en el publicador de Oracle durante la configuración para **@login**y la contraseña para **@password**.  
  
        > [!IMPORTANT]  
        >  Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si almacena credenciales en un archivo de script, debe proteger el archivo para evitar el acceso no autorizado.  
  
    -   Para utilizar autenticación de Windows, especifique el valor **1** para **@security_mode**.  
  
        > [!NOTE]  
        >  Para usar autenticación de Windows, el servidor de Oracle debe estar configurado para admitir conexiones con credenciales de Windows (para obtener más información, vea la documentación de Oracle) y deberá haber iniciado una sesión con la misma cuenta de Microsoft Windows que especificó para el esquema de usuario administrativo de replicación.  
  
4.  Cree un trabajo de Agente de registro del LOG para la base de datos de publicación.  
  
    -   Si no está seguro de si existe un trabajo de Agente de registro del LOG para una base de datos publicada, ejecute [sp_helplogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) en el distribuidor utilizado por el publicador de Oracle, en la base de datos de distribución. Especifique el nombre del publicador de Oracle en **@publisher**. Si el conjunto de resultados está vacío, es necesario crear un trabajo de Agente de registro del LOG.  
  
    -   Si ya existe un trabajo de Agente de registro del LOG para la base de datos de publicación, continúe en el paso 5.  
  
    -   En la base de datos de distribución del distribuidor utilizado por el publicador de Oracle, ejecute [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Especifique las credenciales de Windows con las que se ejecuta el agente para **@job_login** y **@job_password**.  
  
        > [!NOTE]  
        >  La opción **@job_login** debe coincidir con el inicio de sesión proporcionado en el paso 3. No proporcione información de seguridad del editor. El Agente de registro del LOG se conecta al publicador utilizando la información de seguridad proporcionada en el paso 3.  
  
5.  En la base de datos de distribución del distribuidor, ejecute [sp_addpublication &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) para crear la publicación. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  En el distribuidor de la base de datos de distribución, ejecute [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md). Especifique el nombre de publicación usado en el paso 4 para **@publication** y las credenciales de Windows con las que se ejecuta el Agente de instantáneas para **@job_name** y **@password**. Para utilizar la autenticación estándar de Oracle al conectarse al publicador, también debe especificar el valor **0** para **@publisher_security_mode** y la información de inicio de sesión de Oracle para **@publisher_login** y **@publisher_password**. Esto crea un trabajo de Agente de instantáneas para la publicación.  
  
## <a name="see-also"></a>Ver también  
 [Configurar un publicador de Oracle](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Publicar datos y objetos de base de datos](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Configuración del trabajo del conjunto de transacciones para un publicador de Oracle&#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Información general de la publicación de Oracle](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [Script to Grant Oracle Permissions](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  
