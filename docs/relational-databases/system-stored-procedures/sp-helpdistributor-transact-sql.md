---
title: sp_helpdistributor (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpdistributor_TSQL
- sp_helpdistributor
helpviewer_keywords: sp_helpdistributor
ms.assetid: 37b0983e-3b69-4f0f-977e-20efce0a0b97
caps.latest.revision: "32"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f8436c56ec260fdf2f22d5f6ecdb7a1c3102d6be
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpdistributor-transact-sql"></a>sp_helpdistributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra información sobre el distribuidor, la base de datos de distribución, el directorio de trabajo, y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de usuario del agente. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicaciones o en cualquier base de datos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdistributor [ [ @distributor= ] 'distributor' OUTPUT ]  
    [ , [ @distribdb= ] 'distribdb' OUTPUT ]  
    [ , [ @directory= ] 'directory' OUTPUT ]  
    [ , [ @account= ] 'account' OUTPUT ]  
    [ , [ @min_distretention= ] min_distretention OUTPUT ]  
    [ , [ @max_distretention= ] max_distretention OUTPUT ]  
    [ , [ @history_retention= ] history_retention OUTPUT ]  
    [ , [ @history_cleanupagent= ] 'history_cleanupagent' OUTPUT ]  
    [ , [ @distrib_cleanupagent = ] 'distrib_cleanupagent' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]   
    [ , [ @local = ] 'local' ]  
    [ , [ @rpcsrvname= ] 'rpcsrvname' OUTPUT ]  
    [ , [ @publisher_type = ] 'publisher_type' OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@distributor=**] **'***distribuidor***'** salida  
 Es el nombre del distribuidor. El distribuidor es **sysname**, su valor predeterminado es  **%** , que es el único valor que devuelve un conjunto de resultados.  
  
 [  **@distribdb=**] **'***distribdb***'** salida  
 Es el nombre de la base de datos de distribución. *distribdb* es **sysname**, su valor predeterminado es  **%** , que es el único valor que devuelve un conjunto de resultados.  
  
 [  **@directory=**] **'***directorio***'** salida  
 Es el directorio de trabajo. *directorio* es **nvarchar (255)**, su valor predeterminado es  **%** , que es el único valor que devuelve un conjunto de resultados.  
  
 [  **@account=**] **'***cuenta***' salida**  
 Es la cuenta de usuario de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. *cuenta de*es **nvarchar (255)**, su valor predeterminado es  **%** , que es el único valor que devuelve un conjunto de resultados.  
  
 [  **@min_distretention=**] *min_distretention***salida**  
 Es el período mínimo de retención de la distribución en horas. *min_distretention* es **int**, su valor predeterminado es **-1**.  
  
 [  **@max_distretention=**] *max_distretention***salida**  
 Es el período máximo de retención de la distribución en horas. *max_distretention* es **int**, su valor predeterminado es **-1**.  
  
 [  **@history_retention=**] *history_retention***salida**  
 Es el período mínimo de retención del historial en horas. *history_retention* es **int**, su valor predeterminado es **-1**.  
  
 [  **@history_cleanupagent=**] **'***history_cleanupagent***' salida**  
 Es el nombre del agente de limpieza del historial. *history_cleanupagent* es **nvarchar (100)**, su valor predeterminado es  **%** , que es el único valor que devuelve un conjunto de resultados.  
  
 [  **@distrib_cleanupagent =**] **'***distrib_cleanupagent***' salida**  
 Es el nombre del agente de limpieza de distribución. *distrib_cleanupagent* es **nvarchar (100)**, su valor predeterminado es  **%** , que es el único valor que devuelve un conjunto de resultados.  
  
 [  **@publisher=**] **'***publisher***'**  
 Es el nombre del publicador. *Publisher* es **sysname**, su valor predeterminado es null.  
  
 [  **@local=**] **'***local***'**  
 Indica si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe obtener valores del servidor local. *local* es **nvarchar (5)**, su valor predeterminado es null.  
  
 [  **@rpcsrvname=**] **'***rpcsrvname***' salida**  
 Es el nombre del servidor que genera llamadas a procedimientos remotos. *rpcsrvname* es **sysname**, su valor predeterminado es  **%** , que es el único valor que devuelve un conjunto de resultados.  
  
 [  **@publisher_type** =] **'***publisher_type***' salida**  
 Es el tipo de publicador. *publisher_type* es **sysname**, su valor predeterminado es  **%** , que es el único valor que devuelve un conjunto de resultados.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**distribuidor**|**sysname**|Nombre del distribuidor.|  
|**base de datos de distribución**|**sysname**|Nombre de la base de datos de distribución.|  
|**directorio**|**nvarchar(255)**|Nombre del directorio de trabajo.|  
|**cuenta**|**nvarchar(255)**|Nombre de la cuenta de usuario de Windows.|  
|**min distrib retention**|**int**|Período mínimo de retención de la distribución.|  
|**Max distrib retention**|**int**|Período máximo de retención de la distribución.|  
|**retención de historial**|**int**|Período de retención del historial.|  
|**agente de limpieza de historial**|**nvarchar (100)**|Nombre del Agente de limpieza del historial.|  
|**agente de limpieza de distribución**|**nvarchar (100)**|Nombre del Agente de limpieza de distribución.|  
|**nombre del servidor de RPC**|**sysname**|Nombre del distribuidor remoto o local.|  
|**nombre de inicio de sesión de RPC**|**sysname**|Inicio de sesión utilizado por las llamadas a procedimientos remotos al distribuidor remoto.|  
|**tipo de publicador**|**sysname**|Tipo de publicador; puede ser uno de los siguientes:<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **PUERTA DE ENLACE DE ORACLE**|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpdistributor** se utiliza en todos los tipos de replicación.  
  
 Si se especifican uno o varios parámetros de salida al ejecutar **sp_helpdistributor**, todos los parámetros de salida establecidos en NULL se les asignan valores al salir y no se devuelve ningún conjunto de resultados. Si no se especifica ningún parámetro de salida, se devuelve un conjunto de resultados.  
  
## <a name="permissions"></a>Permissions  
 El siguiente conjunto de resultados columnas o parámetros de salida se devuelven a los miembros de la **sysadmin** rol fijo de servidor en el publicador y el **db_owner** rol fijo de base de datos en la base de datos de publicación:  
  
|Columna del conjunto de resultados|Parámetro de salida|  
|-----------------------|----------------------|  
|account |**@account**|  
|min distrib retention|**@min_distretention**|  
|max distrib retention |**@max_distretention**|  
|history retention|**@history_retention**|  
|history cleanup agent|**@history_cleanupagent**|  
|distribution cleanup agent|**@distrib_cleanupagent**|  
|rpc login name|none|  
  
 La siguiente columna de conjuntos de resultados se devuelve a los usuarios de la lista de acceso a la publicación para una publicación en el distribuidor:  
  
-   directory  
  
 Las siguientes columnas de conjuntos de resultados se devuelven a todos los usuarios.  
  
|Columna del conjunto de resultados|Parámetro de salida|  
|-----------------------|----------------------|  
|distributor|**@distributor**|  
|base de datos de distribución|**@distribdb**|  
|rpc server name|**@rpcsrvname**|  
|publisher type|**@publisher_type**|  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar las propiedades del distribuidor y del publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
