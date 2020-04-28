---
title: sp_changereplicationserverpasswords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9feddab12ea972ea4d7764fccfdd91a7f9b89cec
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68762254"
---
# <a name="sp_changereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cambia las contraseñas almacenadas [!INCLUDE[msCoName](../../includes/msconame-md.md)] para la cuenta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Windows o el inicio de sesión que usan los agentes de replicación al conectarse a los servidores de una topología de replicación. Normalmente tendría que cambiar una contraseña para cada agente individual que se ejecutara en un servidor, aunque todos utilizaran el mismo inicio de sesión o la misma cuenta. Este procedimiento almacenado permite cambiar la contraseña para todas las instancias de un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o una cuenta de Windows específicos utilizados por todos los agentes de replicación que se ejecutan en un servidor. Este procedimiento almacenado se ejecuta en cualquier servidor de la topología de replicación de la base de datos maestra.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @login_type = ] login_type`Es el tipo de autenticación de las credenciales proporcionadas. *login_type* es de **tinyint**y no tiene ningún valor predeterminado.  
  
 **1** = autenticación integrada de Windows  
  
 **0** =  0[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación  
  
`[ @login = ] 'login'`Es el nombre de la cuenta de Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el inicio de sesión que se va a cambiar. *login* es **nvarchar (257)** y no tiene ningún valor predeterminado  
  
`[ @password = ] 'password'`Es la nueva contraseña que se va a almacenar para el *Inicio de sesión*especificado. *password* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
> [!NOTE]  
>  Después de cambiar una contraseña de replicación, es necesario detener y reiniciar cada agente que utilice la contraseña para que el cambio surta efecto en dicho agente.  
  
`[ @server = ] 'server'`Es la conexión de servidor para la que se va a cambiar la contraseña almacenada. *Server* es de **tipo sysname**y puede tener uno de estos valores:  
  
|Value|Descripción|  
|-----------|-----------------|  
|**distribuidor**|Todas las conexiones del agente al distribuidor.|  
|**publicador**|Todas las conexiones del agente al publicador.|  
|**suscriptor**|Todas las conexiones del agente al suscriptor.|  
|**%** predeterminada|Todas las conexiones del agente a todos los servidores de una topología de replicación.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 **sp_changereplicationserverpasswords** se usa con todos los tipos de replicación.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_changereplicationserverpasswords**.  
  
## <a name="see-also"></a>Consulte también  
 [Ver y modificar la configuración de seguridad de la replicación](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
