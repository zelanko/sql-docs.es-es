---
title: sp_changesubscriptiondtsinfo (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changesubscriptiondtsinfo
- sp_changesubscriptiondtsinfo_TSQL
helpviewer_keywords:
- sp_changesubscriptiondtsinfo
ms.assetid: 64fc085f-f81b-493b-b59a-ee6192d9736d
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: dbf57f7bc8804863e9f51e3c58c8946d216eaf1d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spchangesubscriptiondtsinfo-transact-sql"></a>sp_changesubscriptiondtsinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades del paquete de Servicios de transformación de datos (DTS) de una suscripción. Este procedimiento almacenado se ejecuta en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_changesubscriptiondtsinfo [ [ @job_id = ] job_id ]  
    [ , [ @dts_package_name= ] 'dts_package_name' ]  
    [ , [ @dts_package_password= ] 'dts_package_password' ]  
    [ , [ @dts_package_location= ] 'dts_package_location' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@job_id=**] *job_id*  
 Es el identificador del trabajo del agente de distribución para la suscripción de inserción. *job_id* es **varbinary (16)**, no tiene ningún valor predeterminado. Para obtener el Id. de trabajo de distribución, ejecute **sp_helpsubscription** o **sp_helppullsubscription**.  
  
 [ **@dts_package_name**=] **'***dts_package_name***'**  
 Especifica el nombre del paquete DTS. *dts_package_name* es un **sysname**, su valor predeterminado es null. Por ejemplo, para especificar un paquete denominado **DTSPub_Package**, especificaría `@dts_package_name = N'DTSPub_Package'`.  
  
 [ **@dts_package_password**=] **'***dts_package_password***'**  
 Especifica la contraseña del paquete. *dts_package_password* es **sysname** con un valor predeterminado es NULL, que especifica que la propiedad de contraseña se debe dejar sin cambios.  
  
> [!NOTE]  
>  Un paquete DTS debe tener una contraseña.  
  
 [ **@dts_package_location**=] **'***dts_package_location***'**  
 Especifica la ubicación del paquete. *dts_package_location* es un **tipo (12)**, su valor predeterminado es null, que especifica que la ubicación del paquete se debe dejar sin cambios. La ubicación del paquete puede cambiarse a **distribuidor** o **suscriptor**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_changesubscriptiondtsinfo** se usa para la replicación de instantáneas y la replicación transaccional sólo las suscripciones de inserción.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor **db_owner** rol fijo de base de datos o el creador de la suscripción puede ejecutar **sp_changesubscriptiondtsinfo**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
