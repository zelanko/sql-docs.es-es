---
title: sp_change_subscription_properties (Transact-SQL) Microsoft Docs
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
ms.openlocfilehash: e033e446fc771ad87542474edb1e90caf08faebd
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528793"
---
# <a name="sp_change_subscription_properties-transact-sql"></a>sp_change_subscription_properties (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Actualiza la información de las suscripciones de extracción. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripciones.  
  
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
`[ @publisher = ] 'publisher'`Es el nombre del publicador. *publisher* es **sysname**, sin valor predeterminado.  
  
`[ @publisher_db = ] 'publisher_db'`Es el nombre de la base de datos del publicador. *publisher_db* es **sysname**, sin valor predeterminado.  
  
`[ @publication = ] 'publication'`Es el nombre de la publicación. *publicación* es **sysname**, sin incumplimiento.  
  
`[ @property = ] 'property'`Es la propiedad que se va a cambiar. *propiedad* es **sysname**.  
  
`[ @value = ] 'value'`Es el nuevo valor de la propiedad. *valor* es **nvarchar(1000)**, sin valor predeterminado.  
  
`[ @publication_type = ] publication_type`Especifica el tipo de replicación de la publicación. *publication_type* es **int**, y puede ser uno de estos valores.  
  
|Value|Tipo de publicación|  
|-----------|----------------------|  
|**0**|Transaccional|  
|**1**|Instantánea|  
|**2**|Merge|  
|NULL (predeterminado)|La replicación determina el tipo de publicación. Puesto que el procedimiento almacenado debe examinar varias tablas, esta opción es más lenta que cuando se suministra el tipo de publicación exacto.|  
  
 En esta tabla se describen las propiedades de los artículos y los valores de esas propiedades.  
  
|Propiedad|Value|Descripción|  
|--------------|-----------|-----------------|  
|**alt_snapshot_folder**||Especifica la ubicación de la carpeta alternativa de la instantánea. Si el valor es NULL, los archivos de instantáneas se toman de la ubicación predeterminada que se especifica en el publicador.|  
|**distrib_job_login**||Inicio de sesión de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows en la que se ejecuta el agente.|  
|**distrib_job_password**||Contraseña de la cuenta de Windows con la que se ejecuta el agente.|  
|**distributor_login**||Inicio de sesión del distribuidor.|  
|**distributor_password**||Contraseña del distribuidor.|  
|**distributor_security_mode**|**1**|Se utiliza la autenticación de Windows para la conexión con el distribuidor.|  
||**0**|Se utiliza la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la conexión con el distribuidor.|  
|**dts_package_name**||Especifica el nombre del paquete de Servicios de transformación de datos (DTS) de SQL Server 2000. Este valor solo puede especificarse si la publicación es transaccional o de instantáneas.|  
|**dts_package_password**||Especifica la contraseña del paquete. *dts_package_password* es **sysname** con un valor predeterminado de NULL, que especifica que la propiedad password debe dejarse sin cambios.<br /><br /> Nota: Un paquete DTS debe tener una contraseña.<br /><br /> Este valor solo puede especificarse si la publicación es transaccional o de instantáneas.|  
|**dts_package_location**||La ubicación donde se almacena el paquete DTS. Este valor solo puede especificarse si la publicación es transaccional o de instantáneas.|  
|**dynamic_snapshot_location**||Especifica la ruta de acceso a la carpeta donde se guardan los archivos de instantáneas. Este valor solo puede especificarse si la publicación es de mezcla.|  
|**ftp_address**||Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**ftp_login**||Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**ftp_password**||Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**ftp_port**||Se conserva únicamente por compatibilidad con versiones anteriores.|  
|**Host**||Nombre del host utilizado al conectarse al publicador.|  
|**internet_login**||Inicio de sesión que utiliza el Agente de mezcla al conectarse al servidor web que hospeda la sincronización web utilizando autenticación básica.|  
|**internet_password**||Contraseña que el Agente de mezcla utiliza cuando se conecta al servidor web que hospeda la sincronización web a través de la autenticación básica.|  
|**internet_security_mode**|**1**|Se utiliza la autenticación de Windows integrada para la sincronización web. Se recomienda utilizar la autenticación básica con sincronización web. Para más información, consulte [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md).|  
||**0**|Se utiliza la autenticación básica para la sincronización web.<br /><br /> Nota: La sincronización web requiere una conexión TLS con el servidor Web.|  
|**internet_timeout**||Duración, en segundos, antes de que expire una solicitud de sincronización web.|  
|**internet_url**||URL que representa la ubicación de la escucha de replicación para la sincronización web.|  
|**merge_job_login**||Inicio de sesión de la cuenta de Windows con la que se ejecuta el agente.|  
|**merge_job_password**||Contraseña de la cuenta de Windows con la que se ejecuta el agente.|  
|**publisher_login**||Inicio de sesión del publicador. Cambiar *publisher_login* solo se admite para las suscripciones para combinar publicaciones.|  
|**publisher_password**||Contraseña del publicador. Cambiar *publisher_password* solo se admite para las suscripciones para combinar publicaciones.|  
|**publisher_security_mode**|**1**|Se utiliza la autenticación de Windows para la conexión con el publicador. Cambiar *publisher_security_mode* solo se admite para las suscripciones para combinar publicaciones.|  
||**0**|Se utiliza la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para la conexión con el publicador.|  
|**use_ftp**|**true**|Utilice FTP en lugar del protocolo normal para recuperar instantáneas.|  
||**false**|Se utiliza el protocolo habitual para recuperar instantáneas.|  
|**use_web_sync**|**true**|Habilita la sincronización web.|  
||**false**|Deshabilita la sincronización web.|  
|**working_directory**||Nombre del directorio de trabajo utilizado para almacenar temporalmente archivos de datos y de esquema para la publicación cuando se utiliza el protocolo de transferencia de archivos (FTP) para transferir archivos de instantáneas.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (éxito) o **1** (fallo)  
  
## <a name="remarks"></a>Observaciones  
 **sp_change_subscription_properties** se utiliza en todos los tipos de replicación.  
  
 **sp_change_subscription_properties** se usa para las suscripciones de extracción.  
  
 Para los publicadores de Oracle, se omite el valor de *publisher_db,* ya que Oracle solo permite una base de datos por instancia del servidor.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** o **db_owner** rol fijo de base de datos pueden ejecutar **sp_change_subscription_properties**.  
  
## <a name="see-also"></a>Consulte también  
 [Ver y modificar las propiedades de la suscripción de extracción](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [sp_addmergepullsubscription &#40;&#41;de Transact-SQLTransact-SQL](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql.md)   
 [sp_addmergepullsubscription_agent &#40;&#41;Transact-SQLTransact-SQL](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)   
 [sp_addpullsubscription &#40;&#41;Transact-SQLTransact-SQL](../../relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql.md)   
 [sp_addpullsubscription_agent &#40;&#41;Transact-SQLTransact-SQL](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
