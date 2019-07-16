---
title: sp_adddistpublisher (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistpublisher
- sp_adddistpublisher_TSQL
helpviewer_keywords:
- sp_adddistpublisher
ms.assetid: 04e15011-a902-4074-b38c-3ec2fc73b838
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5c9cab9530a67b01274bf5d1bafa579199f0a4d8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68072782"
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  Configura un publicador para que utilice una base de datos de distribución determinada. Este procedimiento almacenado se ejecuta en el distribuidor de cualquier base de datos. Tenga en cuenta que los procedimientos almacenados [sp_adddistributor &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) y [sp_adddistributiondb &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) debe ejecutar antes de usar este procedimiento almacenado procedimiento.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_adddistpublisher [ @publisher= ] 'publisher'   
        , [ @distribution_db= ] 'distribution_db'   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @working_directory= ] 'working_directory' ]   
    [ , [ @storage_connection_string= ] 'storage_connection_string']
    [ , [ @trusted= ] 'trusted' ]   
    [ , [ @encrypted_password= ] encrypted_password ]   
    [ , [ @thirdparty_flag = ] thirdparty_flag ]  
    [ , [ @publisher_type = ] 'publisher_type' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @distribution_db = ] 'distribution_db'` Es el nombre de la base de datos de distribución. *distributor_db* es **sysname**, no tiene ningún valor predeterminado. Los agentes de replicación utilizan este parámetro para conectarse al publicador.  
  
`[ @security_mode = ] security_mode` Es el modo de seguridad implementado. Este parámetro solo se usa por los agentes de replicación para conectarse al publicador para suscripciones de actualización en cola o con una que no sean de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publisher. *security_mode* es **int**, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Los agentes de replicación del distribuidor utilizan la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse al publicador.|  
|**1** (predeterminado)|Los agentes de replicación del distribuidor utilizan la autenticación de Windows para conectarse al publicador.|  
  
`[ @login = ] 'login'` Es el inicio de sesión. Este parámetro es obligatorio si *security_mode* es **0**. *login* es de tipo **sysname** y su valor predeterminado es NULL. Los agentes de replicación utilizan este parámetro para conectarse al publicador.  
  
`[ @password = ] 'password']` Es la contraseña. *contraseña* es **sysname**, su valor predeterminado es null. Los agentes de replicación utilizan este parámetro para conectarse al publicador.  
  
> [!IMPORTANT]  
>  No utilice una contraseña en blanco. Utilice una contraseña segura.  
  
`[ @working_directory = ] 'working_directory'` Es el nombre del directorio de trabajo utilizado para almacenar archivos de datos y el esquema para la publicación. *working_directory* es **nvarchar (255)** y el valor predeterminado es la carpeta ReplData para esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por ejemplo `C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData`. El nombre se debe especificar en el formato UNC.  

 Para Azure SQL Database, use `\\<storage_account>.file.core.windows.net\<share>`.

`[ @storage_connection_string = ] 'storage_connection_string'` Es necesario para la base de datos SQL. Usar la clave de acceso desde el Portal de Azure en almacenamiento > configuración.

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]

`[ @trusted = ] 'trusted'` Este parámetro ha quedado en desuso y se proporciona por razones de compatibilidad. *confianza* es **nvarchar (5)** y si se establece en cualquier cosa menos **false** se producirá un error.  
  
`[ @encrypted_password = ] encrypted_password` Establecer *encrypted_password* ya no se admite. Al intentar establecer esto **bit** parámetro **1** se producirá un error.  
  
`[ @thirdparty_flag = ] thirdparty_flag` Indica si el publicador es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *thirdparty_flag* es **bit**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0** (valor predeterminado)|Base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**1**|Otra base de datos distinta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
`[ @publisher_type = ] 'publisher_type'` Especifica el tipo de publicador cuando el publicador no es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publisher_type* es de tipo sysname y puede ser uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (predeterminado).|Especifica un publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ORACLE**|Especifica un publicador estándar de Oracle.|  
|**PUERTA DE ENLACE DE ORACLE**|Especifica un publicador de puerta de enlace de Oracle.|  
  
 Para obtener más información sobre las diferencias entre un publicador de Oracle y un publicador de puerta de enlace de Oracle, vea [configurar un publicador de Oracle](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_adddistpublisher** usa replicación de instantáneas, transaccional y de mezcla.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_adddistpublisher**.  
  
## <a name="see-also"></a>Vea también  
 [Configurar la publicación y la distribución](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Configurar distribución](../../relational-databases/replication/configure-distribution.md)  
  
  
