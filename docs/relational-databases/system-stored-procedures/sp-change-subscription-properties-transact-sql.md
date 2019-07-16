---
title: sp_change_subscription_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_change_subscription_properties_TSQL
- sp_change_subscription_properties
helpviewer_keywords:
- sp_change_subscription_properties
ms.assetid: cf8137f9-f346-4aa1-ae35-91a2d3c16f17
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6152e7f1c1b64cfdeafffe7d5d9eb021bfd4c4a7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68045782"
---
# <a name="spchangesubscriptionproperties-transact-sql"></a>sp_change_subscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Actualiza la información de las suscripciones de extracción. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_change_subscription_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'  
        , [ @property = ] 'property'  
        , [ @value = ] 'value'  
    [ , [ @publication_type = ] publication_type ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publisher = ] 'publisher'` Es el nombre del publicador. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'` Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @publication = ] 'publication'` Es el nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
`[ @property = ] 'property'` Es la propiedad que se puede cambiar. *propiedad* es **sysname**.  
  
`[ @value = ] 'value'` Es el nuevo valor de la propiedad. *valor* es **nvarchar (1000)** , no tiene ningún valor predeterminado.  
  
`[ @publication_type = ] publication_type` Especifica el tipo de replicación de la publicación. *publication_type* es **int**, y puede tener uno de estos valores.  
  
|Valor|Tipo de publicación|  
|-----------|----------------------|  
|**0**|Transaccional|  
|**1**|Snapshot|  
|**2**|Mezcla|  
|NULL (predeterminado)|La replicación determina el tipo de publicación. Puesto que el procedimiento almacenado debe examinar varias tablas, esta opción es más lenta que cuando se suministra el tipo de publicación exacto.|  
  
 En esta tabla se describen las propiedades de los artículos y los valores de esas propiedades.  
  
|Property|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||Especifica la ubicación de la carpeta alternativa de la instantánea. Si el valor es NULL, los archivos de instantáneas se toman de la ubicación predeterminada que se especifica en el publicador.|  
|**distrib_job_login**||Inicio de sesión de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el agente.|  
|**distrib_job_password**||Contraseña de la cuenta de Windows con la que se ejecuta el agente.|  
|**distributor_login**||Inicio de sesión del distribuidor.|  
|**distributor_password**||Contraseña del distribuidor.|  
|**distributor_security_mode**|**1**|Se utiliza la autenticación de Windows para la conexión con el distribuidor.|  
||**0**|Se utiliza la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la conexión con el distribuidor.|  
|**dts_package_name**||Especifica el nombre del paquete de Servicios de transformación de datos (DTS) de SQL Server 2000. Este valor solo puede especificarse si la publicación es transaccional o de instantáneas.|  
|**dts_package_password**||Especifica la contraseña del paquete. *dts_package_password* es **sysname** con el valor predeterminado es NULL, que especifica que la propiedad de contraseña se dejará sin cambios.<br /><br /> Nota: Un paquete DTS debe tener una contraseña.<br /><br /> Este valor solo puede especificarse si la publicación es transaccional o de instantáneas.|  
|**dts_package_location**||La ubicación donde se almacena el paquete DTS. Este valor solo puede especificarse si la publicación es transaccional o de instantáneas.|  
|**dynamic_snapshot_location**||Especifica la ruta de acceso a la carpeta donde se guardan los archivos de instantáneas. Este valor solo puede especificarse si la publicación es de mezcla.|  
|**ftp_address**||Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**ftp_login**||Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**ftp_password**||Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**ftp_port**||Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**Nombre de host**||Nombre del host utilizado al conectarse al publicador.|  
|**internet_login**||Inicio de sesión que utiliza el Agente de mezcla al conectarse al servidor web que hospeda la sincronización web utilizando autenticación básica.|  
|**internet_password**||Contraseña que el Agente de mezcla utiliza cuando se conecta al servidor web que hospeda la sincronización web a través de la autenticación básica.|  
|**internet_security_mode**|**1**|Se utiliza la autenticación de Windows integrada para la sincronización web. Se recomienda utilizar la autenticación básica con sincronización web. Para más información, consulte [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).|  
||**0**|Se utiliza la autenticación básica para la sincronización web.<br /><br /> Nota: La sincronización Web requiere una conexión SSL al servidor Web.|  
|**internet_timeout**||Período de tiempo, en segundos, antes de que expire una solicitud de sincronización Web.|  
|**internet_url**||URL que representa la ubicación de la escucha de replicación para la sincronización web.|  
|**merge_job_login**||Inicio de sesión de la cuenta de Windows con la que se ejecuta el agente.|  
|**merge_job_password**||Contraseña de la cuenta de Windows con la que se ejecuta el agente.|  
|**publisher_login**||Inicio de sesión del publicador. Cambiar *publisher_login* solo se admite para que las suscripciones a publicaciones de combinación.|  
|**publisher_password**||Contraseña del publicador. Cambiar *publisher_password* solo se admite para que las suscripciones a publicaciones de combinación.|  
|**publisher_security_mode**|**1**|Se utiliza la autenticación de Windows para la conexión con el publicador. Cambiar *publisher_security_mode* solo se admite para que las suscripciones a publicaciones de combinación.|  
||**0**|Se utiliza la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la conexión con el publicador.|  
|**use_ftp**|**true**|Utiliza FTP en lugar del protocolo regular para recuperar instantáneas.|  
||**false**|Se utiliza el protocolo habitual para recuperar instantáneas.|  
|**use_web_sync**|**true**|Habilita la sincronización web.|  
||**false**|Deshabilita la sincronización web.|  
|**working_directory**||Nombre del directorio de trabajo utilizado para almacenar temporalmente archivos de datos y de esquema para la publicación cuando se utiliza el protocolo de transferencia de archivos (FTP) para transferir archivos de instantáneas.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_change_subscription_properties** se utiliza en todos los tipos de replicación.  
  
 **sp_change_subscription_properties** se usa para las suscripciones de extracción.  
  
 Para los publicadores de Oracle, el valor de *publisher_db* se omite porque Oracle solo permite una base de datos por cada instancia del servidor.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_change_subscription_properties**.  
  
## <a name="see-also"></a>Vea también  
 [View and Modify Pull Subscription Properties](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)  (Ver y modificar las propiedades de una suscripción de extracción)  
 [sp_addmergepullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_addpullsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
