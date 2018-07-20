---
title: MSsubscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsubscription_properties
- MSsubscription_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_properties system table
ms.assetid: f96fc1ae-b798-4b05-82a7-564ae6ef23b8
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 922651f78062b43bac1262415530068ebde4c7b4
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102393"
---
# <a name="mssubscriptionproperties-transact-sql"></a>MSsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSsubscription_properties** tabla contiene las filas de la información de parámetros necesarios para ejecutar los agentes de replicación en el suscriptor. Esta tabla se almacena en la base de datos de suscripciones en el Suscriptor para una suscripción de extracción o en la base de datos de distribución en el Distribuidor para una suscripción de inserción.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publicador**|**sysname**|El nombre del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publicación**|**sysname**|Nombre de la publicación.|  
|**publication_type**|**int**|Tipo de publicación:<br /><br /> **0** = transaccional.<br /><br /> **2** = la mezcla.|  
|**publisher_login**|**sysname**|Identificador de inicio de sesión utilizado en el publicador para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_password**|**nvarchar (524)**|Contraseña (cifrada) utilizada en el publicador para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**publisher_security_mode**|**int**|Modo de seguridad aplicado en el publicador:<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticación de SQL Server.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] autenticación de Windows.<br /><br /> **2** = los desencadenadores de sincronización utilizan una estática **sysservers** entrada para realizar una llamada a procedimiento remoto (RPC), y *publisher* debe definirse en el **sysservers**tabla como un servidor remoto o vinculado.|  
|**distribuidor**|**sysname**|El nombre del distribuidor.|  
|**distributor_login**|**sysname**|El identificador de inicio de sesión utilizado en el distribuidor para la autenticación de SQL Server.|  
|**distributor_password**|**nvarchar (524)**|Contraseña (cifrada) utilizada en el distribuidor para la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**distributor_security_mode**|**int**|Modo de seguridad aplicado en el distribuidor:<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.<br /><br /> **1** = autenticación de Windows.|  
|**ftp_address**|**sysname**|Dirección de red del servicio FTP (Protocolo de transferencia de archivos) del distribuidor.|  
|**ftp_port**|**int**|El número de puerto del servicio FTP para el distribuidor.|  
|**ftp_login**|**sysname**|El nombre de usuario usada para conectarse al servicio FTP.|  
|**ftp_password**|**nvarchar (524)**|Contraseña u.User usada para conectarse al servicio FTP.|  
|**alt_snapshot_folder**|**nvarchar(255)**|Especifica la ubicación de la carpeta alternativa de la instantánea.|  
|**working_directory**|**nvarchar(255)**|El nombre del directorio de trabajo utilizado para almacenar archivos de datos y el esquema.|  
|**use_ftp**|**bit**|Especifica que se utilizará FTP en lugar del protocolo regular para recuperar las instantáneas. Si **1**, se utiliza FTP.|  
|**dts_package_name**|**sysname**|Especifica el nombre del paquete de Servicios de transformación de datos (DTS).|  
|**dts_package_password**|**nvarchar (524)**|Especifica la contraseña del paquete.|  
|**dts_package_location**|**int**|Ubicación donde se almacena el paquete DTS.|  
|**enabled_for_syncmgr**|**bit**|Especifica si la suscripción se puede sincronizar mediante el Administrador de sincronización de [!INCLUDE[msCoName](../../includes/msconame-md.md)].<br /><br /> **0** = suscripción no está registrada con el Administrador de sincronización.<br /><br /> **1** = suscripción se registra con el Administrador de sincronización y se puede sincronizar sin iniciar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].|  
|**offload_agent**|**bit**|Especifica si el agente puede activarse de manera remota. Si **0**, el agente no puede activarse de forma remota.|  
|**offload_server**|**sysname**|Especifica el nombre de red del servidor utilizado para la activación remota.|  
|**dynamic_snapshot_location**|**nvarchar(255)**|Especifica la ruta de acceso a la carpeta donde se guardan los archivos de instantáneas.|  
|**use_web_sync**|**bit**|Especifica si la suscripción puede sincronizarse mediante HTTP. Un valor de **1** significa que esta característica está habilitada.|  
|**internet_url**|**nvarchar(260)**|Dirección URL que representa la ubicación de la escucha de replicación de la sincronización web.|  
|**internet_login**|**sysname**|El inicio de sesión que utiliza el agente de mezcla al conectarse al servidor Web que hospeda la sincronización Web utilizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.|  
|**internet_password**|**nvarchar (524)**|La contraseña para el inicio de sesión que utiliza el agente de mezcla al conectarse al servidor Web que hospeda la sincronización Web utilizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticación.|  
|**internet_security_mode**|**int**|El modo de autenticación utilizado al conectarse al servidor Web que hospeda la sincronización Web, donde un valor de **1** significa autenticación de Windows y un valor de **0** significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticación.|  
|**internet_timeout**|**int**|Tiempo que transcurre, en segundos, hasta que expira una solicitud de sincronización web.|  
|**Nombre de host**|**sysname**|Especifica el valor de **HOST_NAME** cuando esta función se utiliza en el **donde** cláusula de un filtro de combinación o relación de registros lógicos.|  
  
## <a name="see-also"></a>Vea también  
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
