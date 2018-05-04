---
title: sp_repladdcolumn (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_repladdcolumn_TSQL
- sp_repladdcolumn
helpviewer_keywords:
- sp_repladdcolumn
ms.assetid: d6220f9f-c738-4f9c-bcf8-419994e86c81
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9cf625ec15b26743f956ee94ce39c9facbd7b803
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sprepladdcolumn-transact-sql"></a>sp_repladdcolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega una columna a un artículo de tabla existente que ha sido publicado. Permite agregar la nueva columna a todos los publicadores que publican esta tabla o, simplemente, agregar la columna a una publicación específica que publica la tabla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]  
>  Este procedimiento almacenado ha quedado desusado y se admite por cuestiones de compatibilidad con las versiones anteriores. Solo debe usarse con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] publicadores y [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] los suscriptores de republicación. Este procedimiento no se debería utilizar en columnas con tipos de datos introducidos en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_repladdcolumn [ @source_object = ] 'source_object', [ @column = ] 'column' ]  
    [ , [ @typetext = ] 'typetext' ]  
    [ , [ @publication_to_add = ] 'publication_to_add' ]  
    [ , [ @from_agent = ] from_agent ]  
    [ , [ @schema_change_script = ] 'schema_change_script' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @source_object =] '*source_object*'  
 Es el nombre del artículo de la tabla que contiene la nueva columna que se va a agregar. *source_object* es **nvarchar (358**), no tiene ningún valor predeterminado.  
  
 [ @column =] '*columna*'  
 Es el nombre de la columna de la tabla que se va a agregar para replicación. *columna* es **sysname**, no tiene ningún valor predeterminado.  
  
 [ @typetext =] '*typetext*'  
 Es la definición de la columna que se va a agregar. *TypeText* es **nvarchar (3000)**, no tiene ningún valor predeterminado. Por ejemplo, si se va a agregar la columna order_filled y es un único carácter campo no es NULL y tiene un valor predeterminado de **N**, order_filled sería el *columna* parámetro, mientras que la definición de la columna, **char (1) NOT NULL CONSTRAINT constraint_name DEFAULT ' n '** sería el *typetext* el valor del parámetro.  
  
 [ @publication_to_add =] '*publication_to_add*'  
 Es el nombre de la publicación a la que se agrega la nueva columna. *publication_to_add* es **nvarchar (4000)**, su valor predeterminado es **todos los**. Si **todos los**, a continuación, se ven afectadas todas las publicaciones que contienen esta tabla. Si *publication_to_add* se especifica, solo esta publicación no tiene la nueva columna agregada.  
  
 [ @from_agent =] *from_agent*  
 Si un agente de replicación está ejecutando el procedimiento almacenado. *from_agent* es **int**, su valor predeterminado es **0**, donde un valor de **1** se utiliza cuando se ejecuta este procedimiento almacenado por un agente de replicación y, en cada otro caso, el valor predeterminado de **0**debe utilizarse.  
  
 [ @schema_change_script =] '*el argumento schema_change_script*'  
 Especifica el nombre y la ruta de acceso de un script de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizado para modificar los procedimientos almacenados personalizados generados por el sistema. *el argumento schema_change_script* es **nvarchar (4000)**, su valor predeterminado es null. La replicación permite que los procedimientos almacenados personalizados definidos por el usuario sustituyan a uno o más de los procedimientos predeterminados utilizados en la replicación transaccional. *el argumento schema_change_script* se ejecuta después de un cambio de esquema se realiza en un artículo de tabla replicado mediante sp_repladdcolumn y puede utilizarse para realizar uno de los siguientes:  
  
-   Si los procedimientos almacenados personalizados se generan automáticamente, *el argumento schema_change_script* puede utilizarse para quitar estos procedimientos almacenados personalizados y sustituirlos por otros definidos por el usuario procedimientos almacenados personalizados que admite el nuevo esquema.  
  
-   Si no se generan automáticamente procedimientos almacenados personalizados, *el argumento schema_change_script*puede utilizarse para volver a generar estos procedimientos almacenados o crear personalizado definido por el usuario de los procedimientos almacenados.  
  
 [ @force_invalidate_snapshot =] *force_invalidate_snapshot*  
 Habilita o deshabilita la capacidad de que se invalide una instantánea. *force_invalidate_snapshot* es un **bits**, su valor predeterminado es **1**.  
  
 **1** especifica que los cambios en un artículo pueden invalidar la instantánea no es válida, y si ese es el caso, un valor de **1** concede permiso para la nueva instantánea para que se produzca.  
  
 **0** especifica que los cambios en el artículo no invalidarán la instantánea no es válida.  
  
 [ @force_reinit_subscription =] *force_reinit_subscription*  
 Habilita o deshabilita la capacidad de reinicializar la suscripción. *force_reinit_subscription* es un **bits** con un valor predeterminado de **0**.  
  
 **0** especifica que los cambios en el artículo hacen que la suscripción para reinicializarla.  
  
 **1** especifica que los cambios en el artículo pueden causar la suscripción para reinicializarla, y si ese es el caso, un valor de **1** concede permiso para que se lleve a cabo la reinicialización.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros del rol fijo de servidor sysadmin y del rol fijo de base de datos db_owner pueden ejecutar sp_repladdcolumn.  
  
## <a name="see-also"></a>Vea también  
 [Características en desuso en la replicación de SQL Server](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
