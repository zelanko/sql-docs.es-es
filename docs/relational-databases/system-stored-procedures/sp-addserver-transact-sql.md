---
title: sp_addserver (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addserver
- sp_addserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addserver
- renaming servers
- machine names [SQL Server]
- computer names
ms.assetid: 160a6b29-5e80-44ab-80ec-77d4280f627c
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4263ae95f80518504fca71cf5622b4d3c65c850b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33238502"
---
# <a name="spaddserver-transact-sql"></a>sp_addserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define el nombre de la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando el equipo que hospeda [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es cambiar el nombre, utilice **sp_addserver** para informar a la instancia de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] del nuevo nombre de equipo. Este procedimiento debe ejecutarse en todas las instancias del [!INCLUDE[ssDE](../../includes/ssde-md.md)] hospedado en el equipo. El nombre de instancia de la [!INCLUDE[ssDE](../../includes/ssde-md.md)] no se puede cambiar. Para cambiar el nombre de instancia de una instancia con nombre, instale una instancia nueva con el nombre deseado, desasocie los archivos de base de datos de la instancia antigua, asocie las bases de datos a la nueva instancia y quite la antigua instancia. Como alternativa, puede crear un nombre de alias de cliente en el equipo cliente, redirigir la conexión a un servidor y nombre de instancia diferentes o a la combinación **servidor:puerto** sin cambiar el nombre de la instancia en el equipo servidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_addserver [ @server = ] 'server' ,  
     [ @local = ] 'local'   
     [ , [ @duplicate_ok = ] 'duplicate_OK' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@server =** ] **'***server***'**  
 Es el nombre del servidor. Los nombres de los servidores tienen que ser únicos y cumplir las reglas para los nombres de equipo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, aunque no se permiten espacios. *server* es de tipo **sysname**y no tiene ningún valor predeterminado.  
  
 Cuando varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instalan en un equipo, una instancia opera como si estuviera en un servidor independiente. Especifique una instancia con nombre mediante una referencia a *server* como *nombreDeServidor ombreDeInstancia*.  
  
 [ **@local =** ] **'LOCAL'**  
 Especifica el servidor que se va a agregar como servidor local. **@local** es **varchar (10)**, su valor predeterminado es null. Especificar **@local** como **LOCAL** define **@server** como el nombre del servidor local y el @@SERVERNAME función para devolver el valor de *server*.  
  
 El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] establece esta variable en el nombre del equipo durante la instalación. De forma predeterminada, el nombre del equipo es la forma, los usuarios se conectan a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sin requerir ninguna configuración adicional.  
  
 La definición local solo surte efecto después de reiniciarse el [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Solo puede definirse un servidor local en cada instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 [  **@duplicate_ok =** ] **'duplicate_OK'**  
 Especifica si se permiten nombres de servidor duplicados. **@duplicate_OK** es **varchar (13)**, su valor predeterminado es null. **@duplicate_OK** sólo puede tener el valor **duplicate_OK** o NULL. Si **duplicate_OK** se especifica y el nombre del servidor que se va a agregar ya existe, se produce ningún error. Si no se utilizan parámetros con nombre, **@local** debe especificarse.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="remarks"></a>Comentarios  
 Para establecer o borrar opciones del servidor, utilice **sp_serveroption**.  
  
 **sp_addserver** no se puede usar dentro de una transacción definida por el usuario.  
  
 Usar **sp_addserver** para agregar un servidor remoto ya no está disponible. Use en su lugar [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) .  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol fijo de servidor **setupadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cambia a `ACCOUNTS` la entrada del [!INCLUDE[ssDE](../../includes/ssde-md.md)] para el nombre del equipo que hospeda [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
sp_addserver 'ACCOUNTS', 'local';  
```  
  
## <a name="see-also"></a>Vea también  
 [Cambiar el nombre de un equipo que hospeda una instancia independiente de SQL Server](../../database-engine/install-windows/rename-a-computer-that-hosts-a-stand-alone-instance-of-sql-server.md)   
 [sp_addlinkedserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [sp_dropserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropserver-transact-sql.md)   
 [sp_helpserver & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados de seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)  
  
  
