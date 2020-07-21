---
title: Establecer el método de propagación para los cambios de datos en artículos transaccionales | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transactional replication, propagation methods
- propagating data changes [SQL Server replication]
ms.assetid: 0a291582-f034-42da-a1a3-29535b607b74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a3f8be8b6df1034b06d0aaff6ee61c0c494833c5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060374"
---
# <a name="set-the-propagation-method-for-data-changes-to-transactional-articles"></a>Establecer el método de propagación para cambios de datos en artículos transaccionales
  En este tema se describe cómo establecer el método de propagación para los cambios de datos en artículos transaccionales en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 De forma predeterminada, la replicación transaccional propaga los cambios a los suscriptores mediante un conjunto de procedimientos almacenados para cada artículo. Puede reemplazar estos procedimientos con procedimientos personalizados. Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
-   **Para establecer el método de propagación para los cambios de datos en artículos transaccionales con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Tenga cuidado al editar cualquiera de los archivos de instantáneas generados por la replicación. Debe probar y admitir lógica personalizada en los procedimientos almacenados personalizados. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] no ofrece compatibilidad con lógica personalizada.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 Especifique el método de propagación en la pestaña **propiedades** del cuadro de diálogo **propiedades \<Article> del artículo:** , que está disponible en el Asistente para nueva publicación y en el cuadro de diálogo **propiedades de la publicación: \<Publication> ** . Para obtener más información sobre el uso del asistente y el acceso al cuadro de diálogo, consulte [Create a Publication](create-a-publication.md) (Crear una publicación) y [Ver y modificar propiedades de publicación](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-the-propagation-method"></a>Para especificar el método de propagación  
  
1.  En la página **artículos** del Asistente para nueva publicación o en el cuadro de diálogo **propiedades de la publicación \<Publication> :** , seleccione una tabla y, a continuación, haga clic en **propiedades del artículo**.  
  
2.  Haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
3.  En la **pestaña propiedades** del cuadro de diálogo **propiedades \<Article> del artículo:** , en la sección **entrega de instrucción** , especifique el método de propagación de cada operación con los menús formato de entrega de **inserción**, formato de **entrega de actualización**y formato de **entrega de eliminación** .  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Si está en el cuadro de diálogo **propiedades \<Publication> de la publicación:** , haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
#### <a name="to-generate-and-use-custom-stored-procedures"></a>Para generar y utilizar procedimientos almacenados personalizados  
  
1.  En la página **artículos** del Asistente para nueva publicación o en el cuadro de diálogo **propiedades de la publicación \<Publication> :** , seleccione una tabla y, a continuación, haga clic en **propiedades del artículo**.  
  
2.  Haga clic en **Establecer propiedades del artículo de tabla resaltado**.  
  
     En la **pestaña propiedades** del cuadro de diálogo **propiedades \<Article> del artículo:** , en la sección **entrega de instrucción** , seleccione la sintaxis de llamada en el menú formato de entrega adecuado (**Insertar formato de entrega**, formato de entrega de **actualizaciones**o formato de **entrega de eliminación**) y, a continuación, escriba el nombre del procedimiento que se va a utilizar en el procedimiento almacenado de **inserción**, **eliminar procedimiento**almacenado o **Actualizar**. Para más información sobre la sintaxis CALL, vea la sección "Call syntax for stored procedures" (Sintaxis de llamada para procedimientos almacenados) de [Transactional Articles - Specify How Changes Are Propagated](../transactional/transactional-articles-specify-how-changes-are-propagated.md) (Artículos transaccionales: Especificar cómo se propagan los cambios).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
4.  Si está en el cuadro de diálogo **propiedades \<Publication> de la publicación:** , haga clic en **Aceptar** para guardar y cerrar el cuadro de diálogo.  
  
5.  Cuando se genere la instantánea para la publicación, incluirá el procedimiento que ha especificado en el paso anterior. Los procedimientos utilizarán la sintaxis CALL que ha especificado, pero incluirán la lógica predeterminada que utilice la replicación.  
  
     Después de generar la instantánea, navegue a la carpeta de instantáneas de la publicación a la que pertenece este artículo y busque el archivo **.sch** con el mismo nombre que el artículo. Abra este archivo con el Bloc de notas u otro editor de texto, busque el comando CREATE PROCEDURE para los procedimientos almacenados insert, update o delete, y edite la definición del procedimiento para proporcionar una lógica personalizada para propagar los cambios de datos. Si la instantánea se vuelve a generar, debe volver a crear el procedimiento personalizado.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
 La replicación transaccional le permite controlar cómo los cambios se propagan del publicador a los suscriptores; este método de propagación se puede establecer mediante programación cuando un artículo se crea y se cambia después con los procedimientos almacenados de la replicación.  
  
> [!NOTE]  
>  Puede especificar un método de propagación diferente para cada tipo de operación (inserción, actualización o eliminación) DML (lenguaje de manipulación de datos) que se produce en una fila de datos publicados.  
  
 Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-create-an-article-that-uses-transact-sql-commands-to-propagate-data-changes"></a>Para crear un artículo que use comandos Transact-SQL para propagar cambios de datos  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para la ** \@ publicación**, un nombre para el ** \@ artículo, el objeto de base**de datos que se publica para ** \@ source_object**y un valor de **SQL** para al menos uno de los parámetros siguientes:  
  
    -   ** \@ ins_cmd** : controla la replicación de los comandos [Insert](/sql/t-sql/statements/insert-transact-sql) .  
  
    -   ** \@ upd_cmd** : controla la replicación de los comandos [Update](/sql/t-sql/queries/update-transact-sql) .  
  
    -   ** \@ del_cmd** : controla la replicación de los comandos [Delete](/sql/t-sql/statements/delete-transact-sql) .  
  
    > [!NOTE]  
    >   Al especificar un valor de **SQL** para cualquiera de los parámetros anteriores, los comandos de ese tipo se replicarán al suscriptor como el comando [!INCLUDE[tsql](../../../includes/tsql-md.md)] correspondiente.  
  
     Para más información, consulte [Define an Article](define-an-article.md).  
  
#### <a name="to-create-an-article-that-does-not-propagate-data-changes"></a>Para crear un artículo que no propaga los cambios de datos  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para la ** \@ publicación**, un nombre para el ** \@ artículo, el objeto de base**de datos que se publica para ** \@ source_object**y un valor de **ninguno** para al menos uno de los parámetros siguientes:  
  
    -   ** \@ ins_cmd** : controla la replicación de los comandos [Insert](/sql/t-sql/statements/insert-transact-sql) .  
  
    -   ** \@ upd_cmd** : controla la replicación de los comandos [Update](/sql/t-sql/queries/update-transact-sql) .  
  
    -   ** \@ del_cmd** : controla la replicación de los comandos [Delete](/sql/t-sql/statements/delete-transact-sql) .  
  
    > [!NOTE]  
    >   Al especificar un valor de **NONE** para cualquiera de los parámetros anteriores, los comandos de ese tipo no se replicarán al suscriptor.  
  
     Para más información, consulte [Define an Article](define-an-article.md).  
  
#### <a name="to-create-an-article-with-user-modified-custom-stored-procedures"></a>Para crear un artículo con procedimientos almacenados personalizados modificados por el usuario  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para la ** \@ publicación**, un nombre de artículo para el ** \@ artículo**, el objeto de base de datos que se publica para ** \@ source_object**, un valor para la máscara de ** \@ schema_option** que contiene el valor **0x02** (habilita la generación automática de procedimientos almacenados personalizados) y al menos uno de los parámetros siguientes:  
  
    -   ** \@ ins_cmd** : especifique un valor de <strong>llamada sp_MSins_*article_name*</strong>, donde **_article_name_** es el valor especificado para el ** \@ artículo**.  
  
    -   ** \@ del_cmd** : especifique un valor de <strong>llamada sp_MSdel_*article_name* </strong> o <strong>XCALL sp_MSdel_*article_name*</strong>, donde **_article_name_** es el valor especificado para _ * \@ article * *.  
  
    -   ** \@ upd_cmd** : especifique un valor de <strong>escalal sp_MSupd_*article_name*</strong>, <strong>Call sp_MSupd_*article_name*</strong>, <strong>XCALL sp_MSupd__article_name *</strong> o <strong>MCALL sp_MSupd_* article_name *</strong>, donde _**article_name**_ es el valor especificado para ** \@ article**.  
  
    > [!NOTE]  
    >  Para cada uno de los parámetros de comandos anteriores, puede especificar su propio nombre para los procedimientos almacenados que genera la replicación.  
  
    > [!NOTE]  
    >  Para más información sobre la sintaxis CALL, SCALL, XCALL y MCALL, vea [Transactional Articles - Specify How Changes Are Propagated](../transactional/transactional-articles-specify-how-changes-are-propagated.md) (Artículos transaccionales: Especificar cómo se propagan los cambios).  
  
     Para más información, consulte [Define an Article](define-an-article.md).  
  
2.  Después de generar la instantánea, navegue a la carpeta de instantáneas de la publicación a la que pertenece este artículo y busque el archivo **.sch** con el mismo nombre que el artículo. Abra este archivo con Bloc de notas.exe, busque el comando CREATE PROCEDURE para los procedimientos almacenados de inserción, actualización o eliminación, y edite la definición del procedimiento para proporcionar una lógica personalizada para propagar los cambios de datos. Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-create-an-article-with-custom-scripting-in-the-custom-stored-procedures-to-propagate-data-changes"></a>Para crear un artículo con scripting personalizado en los procedimientos almacenados personalizados y propagar los cambios de datos  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique el nombre de la publicación a la que pertenece el artículo para la ** \@ publicación**, un nombre de artículo para el ** \@ artículo**, el objeto de base de datos que se publica para ** \@ source_object**, un valor para la máscara de ** \@ schema_option** que contiene el valor **0x02** (habilita la generación automática de procedimientos almacenados personalizados) y al menos uno de los parámetros siguientes:  
  
    -   ** \@ ins_cmd** : especifique un valor de <strong>llamada sp_MSins_*article_name*</strong>, donde _**article_name**_ es el valor especificado para el ** \@ artículo**.  
  
    -   ** \@ del_cmd** : especifique un valor de <strong>llamada sp_MSdel_*article_name* </strong> o <strong>XCALL sp_MSdel_*article_name*</strong>, donde _**article_name**_ es el valor especificado para el ** \@ artículo**.  
  
    -   ** \@ upd_cmd** : especifique un valor de <strong>escalal sp_MSupd_*article_name*</strong>, <strong>Call sp_MSupd_*article_name*</strong>, <strong>XCALL sp_MSupd_*article_name*</strong>article_name, <strong>MCALL sp_MSupd_*article_name*</strong>article_name, donde _**article_name**_ es el valor especificado para ** \@ article**.  
  
    > [!NOTE]  
    >  Para cada uno de los parámetros de comandos anteriores, puede especificar su propio nombre para los procedimientos almacenados que genera la replicación.  
  
    > [!NOTE]  
    >  Para más información sobre la sintaxis CALL, SCALL, XCALL y MCALL, vea [Transactional Articles - Specify How Changes Are Propagated](../transactional/transactional-articles-specify-how-changes-are-propagated.md) (Artículos transaccionales: Especificar cómo se propagan los cambios).  
  
     Para más información, consulte [Define an Article](define-an-article.md).  
  
2.  En la base de datos de publicación del publicador, use la instrucción [ALTER PROCEDURE](/sql/t-sql/statements/alter-procedure-transact-sql) para modificar [sp_scriptpublicationcustomprocs](/sql/relational-databases/system-stored-procedures/sp-scriptpublicationcustomprocs-transact-sql) de modo que devuelva un script [CREATE PROCEDURE](/sql/t-sql/statements/create-procedure-transact-sql) para los procedimientos almacenados personalizados de inserción, actualización y eliminación. Para más información, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](../transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
#### <a name="to-change-the-method-of-propagating-changes-for-an-existing-article"></a>Para cambiar el método de propagar los cambios para un artículo existente  
  
1.  En la base de datos de publicación del publicador, ejecute [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql). Especifique ** \@ Publication**, ** \@ article**, un valor de **ins_cmd**, **upd_cmd**o **del_cmd** para ** \@ Property**y el método de propagación adecuado para ** \@ Value**.  
  
2.  Repita el paso 1 para cada método de propagación que se va a cambiar.  
  
## <a name="see-also"></a>Consulte también  
 [Especificar cómo se propagan los cambios para los artículos transaccionales](../transactional/transactional-articles-specify-how-changes-are-propagated.md)   
 [Crear una publicación](create-a-publication.md)  
  
  
