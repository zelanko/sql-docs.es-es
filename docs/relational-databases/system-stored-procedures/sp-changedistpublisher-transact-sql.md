---
title: sp_changedistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 06a0e5e2edb793a94e8d8542ca17734f23824121
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62997815"
---
# <a name="spchangedistpublisher-transact-sql"></a>sp_changedistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades del publicador de distribución. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @storage_connection_string = ] 'storage_connection_string']
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @property = ] 'property'` Es una propiedad para cambiar para el publicador indicado. *propiedad* es **sysname** y puede tener uno de estos valores.  
  
`[ @value = ] 'value'` Es el valor de la propiedad especificada. *valor* es **nvarchar (255)** , su valor predeterminado es null.  
  
`[ @storage_connection_string = ] 'storage_connection_string'` Es necesario para la instancia administrada de SQL Database, debe coincidir con la clave de acceso para el volumen de almacenamiento de Azure SQL Database. 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 En esta tabla se describen las propiedades de los publicadores y los valores de esas propiedades.  
  
|Property|Valores|Descripción|  
|--------------|------------|-----------------|  
|**active**|**true**|Activa el publicador.|  
||**false**|Desactiva el publicador.|  
|**distribution_db**||Nombre de la base de datos de distribución.|  
|**login**||Nombre de inicio de sesión.|  
|**password**||Contraseña segura para el inicio de sesión que se ha proporcionado.|  
|**security_mode**|**1**|Se utiliza la autenticación de Windows para la conexión con el publicador. *No se puede cambiar para que no es* [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publisher.*|  
||**0**|Se utiliza la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la conexión con el publicador. *No se puede cambiar para que no es* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *publisher.*|  
|**working_directory**||Directorio de trabajo utilizado para almacenar archivos de datos y esquemas para la publicación.|  
|NULL (predeterminado)||Todos los disponibles *propiedad* opciones se imprimen.| 
|**storage_connection_string**| Clave de acceso | La clave de acceso para el directorio de trabajo cuando la base de datos Azure SQL Database Managed Instance. 
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changedistpublisher** se utiliza en todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_changedistpublisher**.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
