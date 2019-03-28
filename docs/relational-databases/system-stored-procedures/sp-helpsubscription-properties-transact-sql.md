---
title: sp_helpsubscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a39fe7efd35094330b6885094145b5340bd7f2b8
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527477"
---
# <a name="sphelpsubscriptionproperties-transact-sql"></a>sp_helpsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Recupera información de seguridad de la [MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md) tabla. Este procedimiento almacenado se ejecuta en el suscriptor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publicador* es **sysname**, su valor predeterminado es **%**, que devuelve información acerca de todos los publicadores.  
  
`[ @publisher_db = ] 'publisher_db'` Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, su valor predeterminado es **%**, que devuelve información acerca de todas las bases de datos del publicador.  
  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, su valor predeterminado es **%**, que devuelve información acerca de todas las publicaciones.  
  
`[ @publication_type = ] publication_type` Es el tipo de publicación. *publication_type* es **int**, su valor predeterminado es null. Si se proporciona, *publication_type* debe ser uno de los siguientes valores:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**0**|Publicación transaccional|  
|**1**|Publicación de instantáneas|  
|**2**|Publicación de combinación|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|Nombre del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publication**|**sysname**|Nombre de la publicación.|  
|**publication_type**|**int**|Tipo de publicación:<br /><br /> **0** = transaccional<br /><br /> **1** = instantánea<br /><br /> **2** = la mezcla|  
|**publisher_login**|**sysname**|Id. de inicio de sesión utilizado en el publicador para la Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_password**|**nvarchar(524)**|Contraseña utilizada en el publicador para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (cifrada).|  
|**publisher_security_mode**|**int**|Modo de seguridad utilizado en el publicador.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows|  
|**distributor**|**sysname**|Nombre del distribuidor.|  
|**distributor_login**|**sysname**|Inicio de sesión del distribuidor.|  
|**distributor_password**|**nvarchar(524)**|Contraseña del distribuidor (cifrada).|  
|**distributor_security_mode**|**int**|Modo de seguridad utilizado en el distribuidor:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación<br /><br /> **1** = autenticación de Windows|  
|**ftp_address**|**sysname**|Se conserva únicamente por compatibilidad con versiones anteriores. Dirección de red del servicio de protocolo de transferencia de archivos (FTP) para el distribuidor.|  
|**ftp_port**|**int**|Se conserva únicamente por compatibilidad con versiones anteriores. Número de puerto del servicio FTP para el distribuidor.|  
|**ftp_login**|**sysname**|Se conserva únicamente por compatibilidad con versiones anteriores. Nombre de usuario que se utiliza para conectar con el servicio FTP.|  
|**ftp_password**|**nvarchar(524)**|Se conserva únicamente por compatibilidad con versiones anteriores. Contraseña de usuario que se utiliza para conectar con el servicio FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Especifica la ubicación de la carpeta alternativa de la instantánea.|  
|**working_directory**|**nvarchar(255)**|Nombre del directorio de trabajo utilizado para almacenar archivos de datos y de esquema.|  
|**use_ftp**|**bit**|Especifica que se utilizará FTP en lugar del protocolo regular para recuperar las instantáneas. Si **1**, se utiliza FTP.|  
|**dts_package_name**|**sysame**|Especifica el nombre del paquete de Servicios de transformación de datos (DTS).|  
|**dts_package_password**|**nvarchar(524)**|Especifica la contraseña del paquete, si procede.|  
|**dts_package_location**|**int**|La ubicación donde se almacena el paquete DTS.<br /><br /> **0** = el paquete de ubicación está en el distribuidor.<br /><br /> **1** = el paquete de ubicación está en el suscriptor.|  
|**offload_agent**|**bit**|Especifica si el agente puede activarse de forma remota. Si **0**, el agente no puede activarse de forma remota.|  
|**offload_server**|**sysname**|Especifica el nombre de red del servidor utilizado para la activación remota.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Especifica la ruta de acceso a la carpeta donde se guardan los archivos de instantáneas.|  
|**use_web_sync**|**bit**|Especifica si se puede sincronizar la suscripción a través de HTTPS, el valor **1** significa que esta característica está habilitada.|  
|**internet_url**|**nvarchar(260)**|URL que representa la ubicación de la escucha de replicación para la sincronización web.|  
|**internet_login**|**nvarchar(128)**|Inicio de sesión que utiliza el Agente de mezcla al conectarse al servidor web que hospeda la sincronización web utilizando autenticación básica.|  
|**internet_password**|**nvarchar(524)**|Contraseña para el Inicio de sesión que utiliza el Agente de mezcla al conectarse al servidor web que hospeda la sincronización web utilizando autenticación básica.|  
|**internet_security_mode**|**int**|El modo de autenticación utilizado al conectarse al servidor Web que hospeda la sincronización Web, donde un valor de **1** significa autenticación de Windows y un valor de **0** significa autenticación básica.|  
|**internet_timeout**|**int**|Período de tiempo, en segundos, antes de que expire una solicitud de sincronización Web.|  
|**hostname**|**nvarchar(128)**|Especifica el valor de HOST_NAME() cuando se utiliza esta función en el filtro de fila con parámetros de la cláusula WHERE.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_helpsubscription_properties** se utiliza en la replicación de instantáneas, transaccional y de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_helpsubscription_properties**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
