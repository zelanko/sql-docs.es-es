---
title: sp_repldropcolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repldropcolumn_TSQL
- sp_repldropcolumn
helpviewer_keywords:
- sp_repldropcolumn
ms.assetid: fdc1ec5f-f108-42b4-a2d8-f06a71913ab8
author: stevestein
ms.author: sstein
ms.openlocfilehash: a6b398a4dd7e93521b38708d3a7e37ae09e70a15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771472"
---
# <a name="sp_repldropcolumn-transact-sql"></a>sp_repldropcolumn (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Quita una columna de un artículo de tabla existente que ha sido publicado. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
> [!IMPORTANT]
>  Este procedimiento almacenado ha quedado desusado y se admite fundamentalmente por cuestiones de compatibilidad con las versiones anteriores. Solo se debe usar con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] publicadores y [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] suscriptores de republicación. Este procedimiento no se debería utilizar en columnas con tipos de datos introducidos en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o posterior.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_repldropcolumn [ @source_object = ] 'source_object', [ @column = ] 'column'   
    [ , [ @from_agent = ] from_agent]   
    [ , [ @schema_change_script = ] 'schema_change_script' ]   
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @source_object = ] '*source_object*'  
 Es el nombre del artículo de la tabla que contiene la columna que se va a quitar. *source_object* es de tipo nvarchar (258) y no tiene ningún valor predeterminado.  
  
 [ @column = ] '*columna*'  
 Es el nombre de la columna de la tabla que se va a quitar. la *columna* es de tipo sysname y no tiene ningún valor predeterminado.  
  
 [ @from_agent = ] *from_agent*  
 Si un agente de replicación está ejecutando el procedimiento almacenado. *from_agent* es de tipo int y su valor predeterminado es 0, donde un valor de 1 se utiliza cuando un agente de replicación está ejecutando este procedimiento almacenado y, en cualquier otro caso, se debe usar el valor predeterminado de 0.  
  
 [ @schema_change_script = ] '*schema_change_script*'  
 Especifica el nombre y la ruta de acceso de un script de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizado para modificar los procedimientos almacenados personalizados generados por el sistema. *schema_change_script* es de tipo nvarchar (4000) y su valor predeterminado es NULL. La replicación permite que los procedimientos almacenados personalizados definidos por el usuario sustituyan a uno o más de los procedimientos predeterminados utilizados en la replicación transaccional. *schema_change_script* se ejecuta después de realizar un cambio de esquema en un artículo de tabla replicada mediante sp_repldropcolumn y se puede usar para realizar una de las acciones siguientes:  
  
-   Si los procedimientos almacenados personalizados se vuelven a generar automáticamente, *schema_change_script* se pueden utilizar para quitar estos procedimientos almacenados personalizados y reemplazarlos con procedimientos almacenados personalizados definidos por el usuario que admitan el nuevo esquema.  
  
-   Si los procedimientos almacenados personalizados no se vuelven a generar automáticamente, *schema_change_script*se pueden usar para volver a generar estos procedimientos almacenados o para crear procedimientos almacenados personalizados definidos por el usuario.  
  
 [ @force_invalidate_snapshot = ] *force_invalidate_snapshot*  
 Habilita o deshabilita la capacidad de que se invalide una instantánea. *force_invalidate_snapshot* es un bit, con un valor predeterminado de 1.  
  
 El valor 1 significa que, al cambiar un artículo, la instantánea puede quedar invalidada y, en tal caso, el valor 1 concede el permiso necesario para que se produzca la nueva instantánea.  
  
 0 especifica que los cambios en el artículo no invalidarán la instantánea.  
  
 [ @force_reinit_subscription = ] *force_reinit_subscription*  
 Habilita o deshabilita la capacidad de reinicializar la suscripción. *force_reinit_subscription* es un bit con un valor predeterminado de 0.  
  
 0 especifica que los cambios en el artículo no harán que se reinicialice la suscripción.  
  
 1 significa que los cambios en un artículo pueden hacer que la suscripción se reinicialice y, en tal caso, el valor 1 concede el permiso necesario para que se reinicialice la suscripción.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor sysadmin en el publicador o los miembros de los roles fijos de base de datos db_owner o db_ddladmin de la base de datos de publicaciones pueden ejecutar sp_repldropcolumn.  
  
## <a name="see-also"></a>Consulte también  
 [Características desusadas en Replicación de SQL Server](../../relational-databases/replication/deprecated-features-in-sql-server-replication.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
