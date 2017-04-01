---
title: "Establecer el m&#233;todo de propagaci&#243;n para cambios de datos en art&#237;culos transaccionales | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "replicación transaccional, métodos de propagación"
  - "propagar cambios de datos [replicación de SQL Server]"
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Establecer el m&#233;todo de propagaci&#243;n para cambios de datos en art&#237;culos transaccionales
  En este tema se describe cómo establecer el método de propagación para los cambios de datos en artículos transaccionales en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 De forma predeterminada, la replicación transaccional propaga los cambios a los suscriptores mediante un conjunto de procedimientos almacenados para cada artículo. Puede reemplazar estos procedimientos con procedimientos personalizados. Para obtener más información, consulte [especificar cómo se propagan los cambios en los artículos transaccionales](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para establecer el método de propagación para los cambios de datos en artículos transaccionales con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Tenga cuidado al editar cualquiera de los archivos de instantáneas generados por la replicación. Debe probar y admitir lógica personalizada en los procedimientos almacenados personalizados. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] no ofrece compatibilidad con lógica personalizada.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 Especificar el método de propagación en la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo, que está disponible en el Asistente para nueva publicación y la **Propiedades de la publicación - \< publicación>** cuadro de diálogo. Para obtener más información sobre cómo usar el asistente y acceso al cuadro de diálogo, vea [crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md) y [Ver y modificar propiedades de publicación](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar el método de propagación  
  
1.  En el **artículos** página del Asistente para nueva publicación o **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione una tabla y, a continuación, haga clic en **Propiedades del artículo**.  
  
2.  Haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
3.  En la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo el **entrega de instrucción** especifique el método de propagación para cada operación utilizando la **formato de entrega de INSERCIÓN**, **formato de entrega de actualización**, y **formato de entrega de eliminación** menús.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### Para generar y utilizar procedimientos almacenados personalizados  
  
1.  En el **artículos** página del Asistente para nueva publicación o **Propiedades de la publicación - \< publicación>** cuadro de diálogo, seleccione una tabla y, a continuación, haga clic en **Propiedades del artículo**.  
  
2.  Haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
     En la **propiedades** ficha de la **Propiedades del artículo: \< artículo>** cuadro de diálogo el **entrega de instrucción** seleccione la sintaxis de llamada en el menú Formato de entrega adecuado (**formato de entrega de INSERCIÓN**, **formato de entrega de actualización**, o **formato de entrega de eliminación**) y, a continuación, escriba el nombre del procedimiento que se va a usar en **procedimiento almacenado INSERT**, **procedimiento almacenado de eliminación**, o **procedimiento almacenado de actualización**. Para obtener más información acerca de la sintaxis de llamada, consulte la sección "Sintaxis de llamada para los procedimientos almacenados" en [especificar cómo se propagan los cambios en los artículos transaccionales](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  Si se encuentra en la **Propiedades de la publicación - \< publicación>** cuadro de diálogo, haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
5.  Cuando se genere la instantánea para la publicación, incluirá el procedimiento que ha especificado en el paso anterior. Los procedimientos utilizarán la sintaxis CALL que ha especificado, pero incluirán la lógica predeterminada que utilice la replicación.  
  
     Después de generar la instantánea, navegue a la carpeta de instantáneas de la publicación a la que pertenece este artículo y busque el archivo **.sch** con el mismo nombre que el artículo. Abra este archivo con el Bloc de notas u otro editor de texto, busque el comando CREATE PROCEDURE para los procedimientos almacenados insert, update o delete, y edite la definición del procedimiento para proporcionar una lógica personalizada para propagar los cambios de datos. Si la instantánea se vuelve a generar, debe volver a crear el procedimiento personalizado.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 La replicación transaccional le permite controlar cómo los cambios se propagan del publicador a los suscriptores; este método de propagación se puede establecer mediante programación cuando un artículo se crea y se cambia después con los procedimientos almacenados de la replicación.  
  
> [!NOTE]  
>  Puede especificar un método de propagación diferente para cada tipo de operación (inserción, actualización o eliminación) DML (lenguaje de manipulación de datos) que se produce en una fila de datos publicados.  
  
 Para obtener más información, consulte [especificar cómo se propagan los cambios en los artículos transaccionales](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### Para crear un artículo que use comandos Transact-SQL para propagar cambios de datos  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se publica para **@source_object**, y un valor de **SQL** para al menos uno de los siguientes parámetros:  
  
    -   **@ins_cmd** -controla la replicación de [Insertar](../../../t-sql/statements/insert-transact-sql.md) comandos.  
  
    -   **@upd_cmd** -controla la replicación de [actualización](../../../t-sql/queries/update-transact-sql.md) comandos.  
  
    -   **@del_cmd** -controla la replicación de [Eliminar](../../../t-sql/statements/delete-transact-sql.md) comandos.  
  
    > [!NOTE]  
    >  Al especificar un valor de **SQL** para cualquiera de los parámetros anteriores, comandos de ese tipo se replicarán al suscriptor como adecuado [!INCLUDE[tsql](../../../includes/tsql-md.md)] comando.  
  
     Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para crear un artículo que no propaga los cambios de datos  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se publica para **@source_object**, y un valor de **NONE** para al menos uno de los siguientes parámetros:  
  
    -   **@ins_cmd** -controla la replicación de [Insertar](../../../t-sql/statements/insert-transact-sql.md) comandos.  
  
    -   **@upd_cmd** -controla la replicación de [actualización](../../../t-sql/queries/update-transact-sql.md) comandos.  
  
    -   **@del_cmd** -controla la replicación de [Eliminar](../../../t-sql/statements/delete-transact-sql.md) comandos.  
  
    > [!NOTE]  
    >  Al especificar un valor de **NONE** para cualquiera de los parámetros anteriores, los comandos de ese tipo no se replican al suscriptor.  
  
     Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### Para crear un artículo con procedimientos almacenados personalizados modificados por el usuario  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se publica para **@source_object**, un valor para el **@schema_option** máscara de bits que contiene el valor **0 x 02** (permite la generación automática de procedimientos almacenados personalizados) y al menos uno de los siguientes parámetros:  
  
    -   **@ins_cmd** -Especifique un valor de **CALL sp_MSins_*article_name***, donde ***article_name*** es el valor especificado para **@article**.  
  
    -   **@del_cmd** -Especifique un valor de **llamada sp_MSdel_*article_name*** o **XCALL sp_MSdel_*article_name***, donde ***article_name*** es el valor especificado para **@article**.  
  
    -   **@upd_cmd** -Especifique un valor de **SCALL sp_MSupd_*article_name***, **sp_MSupd_ llamada*article_name***, **XCALL sp_MSupd_*article_name***, o **MCALL sp_MSupd_*article_name***, donde ***article_name*** es el valor especificado para **@article**.  
  
    > [!NOTE]  
    >  Para cada uno de los parámetros de comandos anteriores, puede especificar su propio nombre para los procedimientos almacenados que genera la replicación.  
  
    > [!NOTE]  
    >  Para obtener más información acerca de la sintaxis de llamada, SCALL, XCALL y MCALL, vea [especificar cómo se propagan los cambios en los artículos transaccionales](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
     Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  Después de generar la instantánea, navegue a la carpeta de instantáneas de la publicación a la que pertenece este artículo y busque el archivo **.sch** con el mismo nombre que el artículo. Abra este archivo con Bloc de notas.exe, busque el comando CREATE PROCEDURE para los procedimientos almacenados de inserción, actualización o eliminación, y edite la definición del procedimiento para proporcionar una lógica personalizada para propagar los cambios de datos. Para obtener más información, consulte [especificar cómo se propagan los cambios en los artículos transaccionales](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### Para crear un artículo con scripting personalizado en los procedimientos almacenados personalizados y propagar los cambios de datos  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique el nombre de la publicación a la que pertenece el artículo para **@publication**, un nombre de artículo para **@article**, el objeto de base de datos que se publica para **@source_object**, un valor para el **@schema_option** máscara de bits que contiene el valor **0 x 02** (permite la generación automática de procedimientos almacenados personalizados) y al menos uno de los siguientes parámetros:  
  
    -   **@ins_cmd** -Especifique un valor de **CALL sp_MSins_*article_name***, donde ***article_name*** es el valor especificado para **@article**.  
  
    -   **@del_cmd** -Especifique un valor de **llamada sp_MSdel_*article_name*** o **XCALL sp_MSdel_*article_name***, donde ***article_name*** es el valor especificado para **@article**.  
  
    -   **@upd_cmd** -Especifique un valor de **SCALL sp_MSupd_*article_name***, **sp_MSupd_ llamada*article_name***, **XCALL sp_MSupd_*article_name***, **MCALL sp_MSupd_*article_name***, donde ***article_name*** es el valor especificado para **@article**.  
  
    > [!NOTE]  
    >  Para cada uno de los parámetros de comandos anteriores, puede especificar su propio nombre para los procedimientos almacenados que genera la replicación.  
  
    > [!NOTE]  
    >  Para obtener más información acerca de la sintaxis de llamada, SCALL, XCALL y MCALL, vea [especificar cómo se propagan los cambios en los artículos transaccionales](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
     Para más información, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
2.  En el publicador de la base de datos de publicación, use el [ALTER PROCEDURE](../../../t-sql/statements/alter-procedure-transact-sql.md) instrucción editar [sp_scriptpublicationcustomprocs](../../../relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql.md) para que devuelva un [CREATE PROCEDURE](../../../t-sql/statements/create-procedure-transact-sql.md) secuencia de comandos de inserción, actualización y procedimientos almacenados personalizados de la eliminación. Para obtener más información, consulte [especificar cómo se propagan los cambios en los artículos transaccionales](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md).  
  
#### Para cambiar el método de propagar los cambios para un artículo existente  
  
1.  En el publicador de la base de datos de publicación, ejecute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Especifique **@publication**, **@article**, un valor de **ins_cmd**, **upd_cmd**, o **del_cmd** para **@property**, y el método de propagación adecuado para **@value**.  
  
2.  Repita el paso 1 para cada método de propagación que se va a cambiar.  
  
## Vea también  
 [Especificar cómo se propagan los cambios para los artículos transaccionales](../../../relational-databases/replication/transactional/specify-how-changes-are-propagated-for-transactional-articles.md)   
 [Crear, modificar y eliminar publicaciones y artículos & #40; Replicación y nº 41;](../../../relational-databases/replication/publish/create-modify-and-delete-publications-and-articles-replication.md)  
  
  