---
title: sp_changemergepublication (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_changemergepublication_TSQL
- sp_changemergepublication
helpviewer_keywords:
- sp_changemergepublication
ms.assetid: 81fe1994-7678-4852-980b-e02fedf1e796
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 919e55df9dce3384b2a9eea6f5052ca25c094ac3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47758743"
---
# <a name="spchangemergepublication-transact-sql"></a>sp_changemergepublication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de una publicación de combinación. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changemergepublication [ @publication= ] 'publication'  
    [ , [ @property= ] 'property' ]  
    [ , [ @value= ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicación***'**  
 Nombre de la publicación. *publicación* es **sysname**, no tiene ningún valor predeterminado.  
  
 [  **@property=**] **'***propiedad***'**  
 La propiedad que se va a cambiar para la publicación especificada. *propiedad* es **sysname**, y puede ser uno de los valores que aparecen en la tabla siguiente.  
  
 [  **@value=**] **'***valor***'**  
 El nuevo valor de la propiedad especificada. *valor* es **nvarchar (255)**, y puede ser uno de los valores que aparecen en la tabla siguiente.  
  
 Esta tabla describe las propiedades de la publicación que se pueden cambiar, así como las restricciones de los valores de esas propiedades.  
  
|Property|Valor|Descripción|  
|--------------|-----------|-----------------|  
|**allow_anonymous**|**true**|Se admiten las suscripciones anónimas.|  
||**False**|No se admiten las suscripciones anónimas.|  
|**allow_partition_realignment**|**true**|Las eliminaciones se envían al suscriptor para reflejar los resultados de un cambio en la partición mediante la eliminación de los datos que han dejado de formar parte de la partición del suscriptor. Éste es el comportamiento predeterminado.|  
||**False**|Los datos de la partición antigua se dejan en el suscriptor, donde los cambios realizados en estos datos del publicador no se replican en este suscriptor. En cambio, los cambios realizados en el suscriptor se replican en el publicador. Esto sirve para conservar los datos de una partición antigua en una suscripción cuando es necesario que los datos estén accesibles con fines históricos.|  
|**allow_pull**|**true**|Se permiten suscripciones de extracción para la publicación indicada.|  
||**False**|No se permiten suscripciones de extracción para la publicación indicada.|  
|**allow_push**|**true**|Se permiten suscripciones de inserción para la publicación indicada.|  
||**False**|No se permiten suscripciones de inserción para la publicación indicada.|  
|**allow_subscriber_initiated_snapshot**|**true**|El suscriptor puede iniciar el proceso de instantáneas.|  
||**False**|El suscriptor no puede iniciar el proceso de instantáneas.|  
|**allow_subscription_copy**|**true**|Puede copiar las bases de datos de suscripciones suscritas a esta publicación.|  
||**False**|No puede copiar las bases de datos de suscripciones suscritas a esta publicación.|  
|**allow_synctoalternate**|**true**|Permite que un asociado de sincronización alternativo se sincronice con este publicador.|  
||**False**|No permite que un modelo de sincronización alternativo se sincronice con este publicador.|  
|**allow_web_synchronization**|**true**|Las suscripciones se pueden sincronizar por HTTPS.|  
||**False**|Las suscripciones no se pueden sincronizar por HTTPS.|  
|**alt_snapshot_folder**||Especifica la ubicación de la carpeta alternativa para la instantánea.|  
|**automatic_reinitialization_policy**|**1**|Los cambios se cargan desde el suscriptor antes de reinicializar la suscripción.|  
||**0**|La suscripción se reinicializa sin cargar primero los cambios.|  
|**centralized_conflicts**|**true**|Todos los registros de conflictos se almacenan en el publicador. Si cambia esta propiedad, se deben reinicializar los suscriptores existentes.|  
||**False**|Los registros de conflictos se almacenan en el servidor que perdió en la resolución de conflictos. Si cambia esta propiedad, se deben reinicializar los suscriptores existentes.|  
|**compress_snapshot**|**true**|La instantánea de una carpeta de instantáneas alternativa se comprime en formato CAB. La instantánea de la carpeta de instantáneas predeterminada no se puede comprimir. Para cambiar esta propiedad, se requiere una instantánea nueva.|  
||**False**|De forma predeterminada, no se comprime la instantánea. Para cambiar esta propiedad, se requiere una instantánea nueva.|  
|**conflict_logging**|**publicador**|Los registros de conflictos se almacenan en el publicador.|  
||**suscriptor**|Los registros de conflictos se almacenan en el suscriptor que causó el conflicto. No se admite para [!INCLUDE[ssEW](../../includes/ssew-md.md)] suscriptores *.*|  
||**ambos**|Los registros de conflictos se almacenan tanto en el publicador como en el suscriptor.|  
|**conflict_retention**||Un **int** que especifica el período de retención en días, para el que se conservan los conflictos. Establecer *conflict_retention* a **0** significa que no es necesaria ninguna limpieza de conflictos.|  
|**Descripción**||Descripción de la publicación.|  
|**dynamic_filters**|**true**|La publicación se filtra según una cláusula dinámica.|  
||**False**|La publicación no se filtra dinámicamente.|  
|**enabled_for_internet**|**true**|La publicación para Internet está habilitada. El protocolo de transferencia de archivos (FTP) se puede utilizar para transferir los archivos de instantáneas a un suscriptor. Los archivos de sincronización para la publicación se colocan en el directorio C:\Program Files\Microsoft SQL Server\MSSQL\Repldata\ftp.|  
||**False**|No se habilita la publicación para Internet.|  
|**ftp_address**||Dirección de red del servicio FTP para el distribuidor. Especifica la ubicación de los archivos de instantáneas de la publicación.|  
|**ftp_login**||Nombre de usuario que se usa para conectarse al servicio FTP.|  
|**ftp_password**||Contraseña de usuario que se usa para conectarse al servicio FTP.|  
|**ftp_port**||El número de puerto del servicio FTP para el distribuidor. Especifica el número del puerto TCP del sitio FTP donde se almacenan los archivos de instantáneas de la publicación.|  
|**ftp_subdirectory**||Especifica dónde se crean los archivos de instantáneas si la publicación admite la propagación de instantáneas mediante FTP.|  
|**generation_leveling_threshold**|**int**|Especifica el número de cambios que se encuentran en una generación. Una generación es un conjunto de cambios que se entregan a un publicador o suscriptor.|  
|**keep_partition_changes**|**true**|La sincronización se optimiza y solo se ven afectados los suscriptores que tienen filas en las particiones que han cambiado. Para cambiar esta propiedad, se requiere una instantánea nueva.|  
||**False**|La sincronización no se optimiza y las particiones que se envían a todos los suscriptores se comprueban cuando los datos cambian en una partición. Para cambiar esta propiedad, se requiere una instantánea nueva.|  
|**max_concurrent_merge**||Se trata de un **int** que representa el número máximo de procesos de mezcla simultáneos que se pueden ejecutar con una publicación. Si es 0, no hay límite. Si se programa un número de procesos de mezcla superior a éste para que se ejecuten a la vez, el exceso de trabajos se coloca en una cola y se espera hasta que termine de procesarse la mezcla que se está ejecutando.|  
|**max_concurrent_dynamic_snapshots**||Se trata de un **int** que representa el número máximo de sesiones de instantáneas para generar los datos filtrados de instantánea que puede ejecutar simultáneamente con una publicación de mezcla que utiliza filtros de filas con. Si **0**, no hay ningún límite. Si se programa un número de procesos de instantáneas superior a éste para que se ejecuten a la vez, el exceso de trabajos se coloca en una cola y se espera hasta que termine de procesarse la mezcla que se está ejecutando.|  
|**post_snapshot_script**||Especifica un puntero a un **.sql** ubicación del archivo. El Agente de distribución o el Agente de mezcla ejecutan el script posterior a la instantánea después de que se aplique el resto de scripts de objetos replicados y datos durante la sincronización inicial. Para cambiar esta propiedad, se requiere una instantánea nueva.|  
|**pre_snapshot_script**||Especifica un puntero a un **.sql** ubicación del archivo. El Agente de mezcla ejecuta el script previo a la instantánea antes que cualquiera de los scripts de objetos replicados al aplicar la instantánea en un suscriptor. Para cambiar esta propiedad, se requiere una instantánea nueva.|  
|**publication_compatibility_level**|**100RTM**|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
||**90RTM**|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]|  
|**publish_to_ActiveDirectory**|**true**|Este parámetro ha quedado desusado y solo se admite para la compatibilidad de scripts con versiones anteriores. Ya no es posible agregar información de publicación a Active Directory.|  
||**False**|Quita la información de publicaciones de Active Directory.|  
|**replicate_ddl**|**1**|Las instrucciones de lenguaje de definición de datos (DDL) que se ejecutan en el publicador se replican.|  
||**0**|Las instrucciones de DDL no se replican.|  
|**retención**||Se trata de un **int** que representa el número de *retention_period_unit* unidades para el que se va a guardar los cambios para la publicación indicada. Si la suscripción no está sincronizada en el período de retención y se han quitado, por medio de una operación de limpieza en el distribuidor, los cambios pendientes que podía haber recibido, la suscripción expira y es necesario reinicializarla. El período de retención máximo admitido es el número de días entre el 31 de diciembre de 9999 y la fecha actual.<br /><br /> Nota: El período de retención para las publicaciones de combinación tiene un período de gracia de 24 horas para dar cabida a los suscriptores en diferentes zonas horarias.|  
|**retention_period_unit**|**day**|El período de retención se especifica en días.|  
||**week**|El período de retención se especifica en semanas.|  
||**month**|El período de retención se especifica en meses.|  
||**year**|El período de retención se especifica en años.|  
|**snapshot_in_defaultfolder**|**true**|Los archivos de instantánea se almacenan en la carpeta de instantáneas predeterminada.|  
||**False**|Los archivos de instantánea se almacenan en la ubicación alternativa especificada por *alt_snapshot_folder*. Esta combinación especifica que los archivos de instantáneas se almacenan tanto en la ubicación predeterminada como en la alternativa.|  
|**snapshot_ready**|**true**|Está disponible la instantánea para la publicación.|  
||**False**|No está disponible la instantánea para la publicación.|  
|**status**|**Active**|La publicación está en estado activo.|  
||**inactivo**|La publicación está en estado inactivo.|  
|**sync_mode**|**nativo** o<br /><br /> **bcp nativo**|La salida del programa de copia masiva de todas las tablas en modo nativo se utiliza para la instantánea inicial.|  
||**carácter**<br /><br /> o **carácter bcp**|La salida del programa de copia masiva de todas las tablas en modo de carácter se utiliza para la instantánea inicial, que se necesita para todos los suscriptores que no lo son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**use_partition_groups**<br /><br /> Nota: después de utilizar partition_groups, si se revierte al uso **setupbelongs**y establezca **use_partition_groups = false** en **changemergearticle**, esto podría no ser refleja correctamente después de tomar una instantánea. Los desencadenadores que genera una instantánea son conformes con los grupos de particiones.<br /><br /> La solución para este escenario consiste en establecer el estado en Inactive, modificar el **use_partition_groups**y, a continuación, establezca el estado en activo.|**true**|La publicación utiliza particiones previamente calculadas.|  
||**False**|La publicación no utiliza particiones previamente calculadas.|  
|**validate_subscriber_info**||Muestra las funciones que se utilizan para recuperar información del suscriptor. Después, valida los criterios de filtro dinámico que se están utilizando para que el suscriptor compruebe que la información se está dividiendo de un modo coherente.|  
|**web_synchronization_url**||Valor predeterminado de la URL de Internet utilizada para la sincronización web.|  
|NULL (predeterminado)||Devuelve la lista de valores admitidos para *propiedad*.|  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 Confirma que la acción realizada por este procedimiento almacenado puede invalidar una instantánea existente. *force_invalidate_snapshot* es un **bit**, su valor predeterminado es **0**.  
  
 **0** especifica que el cambio de la publicación no invalidan la instantánea. Si el procedimiento almacenado detecta que el cambio requiere una nueva instantánea, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que el cambio de la publicación, es posible que invvalidate la instantánea. Si hay suscripciones existentes que requieran una nueva instantánea, se da permiso para que la instantánea existente se marque como obsoleta y se genere otra nueva.  
  
 Vea en la sección de Observaciones las propiedades que, si se cambian, requieren que se genere una nueva instantánea.  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 Confirma que la acción realizada por este procedimiento almacenado puede requerir la reinicialización de las suscripciones existentes. *force_reinit_subscription* es un **bit** con un valor predeterminado de **0**.  
  
 **0** especifica que el cambio de la publicación no requiere que se reinicialicen las suscripciones. Si el procedimiento almacenado detecta que el cambio requiere la reinicialización de las suscripciones existentes, se producirá un error y no se realizarán cambios.  
  
 **1** especifica que el cambio hace que la publicación se reinicialicen las suscripciones existentes y concede permiso para que se produzca la reinicialización de suscripción.  
  
 Vea en la sección de Notas las propiedades que, si se cambian, requieren que se reinicialicen todas las suscripciones existentes.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changemergepublication** se utiliza en la replicación de mezcla.  
  
 Si se cambian las propiedades siguientes, se requiere que se genere una nueva instantánea. Debe especificar un valor de **1** para el *force_invalidate_snapshot* parámetro.  
  
-   **alt_snapshot_folder**  
  
-   **compress_snapshot**  
  
-   **dynamic_filters**  
  
-   **ftp_address**  
  
-   **ftp_login**  
  
-   **ftp_password**  
  
-   **ftp_port**  
  
-   **ftp_subdirectory**  
  
-   **post_snapshot_script**  
  
-   **valor de publication_compatibility_level** (a **80SP3** sólo)  
  
-   **pre_snapshot_script**  
  
-   **snapshot_in_defaultfolder**  
  
-   **sync_mode**  
  
-   **use_partition_groups**  
  
 Al cambiar las propiedades siguientes, se requiere que se reinicialicen las suscripciones existentes. Debe especificar un valor de **1** para el *force_reinit_subscription* parámetro.  
  
-   **dynamic_filters**  
  
-   **validate_subscriber_info**  
  
 Para enumerar los objetos de publicación a Active Directory mediante el uso de la *publish_to_active_directory*, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya se debe crear el objeto en Active Directory.  
  
## <a name="example"></a>Ejemplo  
 [!code-sql[HowTo#sp_changemergepublication](../../relational-databases/replication/codesnippet/tsql/sp-changemergepublicatio_1.sql)]  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos se puede ejecutar **sp_changemergepublication**.  
  
## <a name="see-also"></a>Vea también  
 [Ver y modificar propiedades de publicación](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Cambiar las propiedades de la publicación y de los artículos](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [sp_addmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)   
 [sp_dropmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md)   
 [sp_helpmergepublication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md)   
 [Procedimientos almacenados de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
