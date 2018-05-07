---
title: sp_publisherproperty (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_publisherproperty
- sp_publisherproperty_TSQL
helpviewer_keywords:
- sp_publisherproperty
ms.assetid: 0ed1ebc1-a1bd-4aed-9f46-615c5cf07827
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 647bd0de356a8a31c531a027dffeca88cd8c3083
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sppublisherproperty-transact-sql"></a>sp_publisherproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra o cambia las propiedades del publicador para no -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores. Este procedimiento almacenado se ejecuta en el distribuidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@publisher** =] **'***publisher***'**  
 Es el nombre del publicador heterogéneo. *Publisher* es **sysname**, no tiene ningún valor predeterminado.  
  
 [**@propertyname** =] **'***propertyname***'**  
 Es el nombre de la propiedad que se va a establecer. *PropertyName* es **sysname**, y puede tener uno de los siguientes valores.  
  
|Value|Description|  
|-----------|-----------------|  
|**xactsetbatching**|Si las transacciones en el publicador están agrupadas en conjuntos transaccionalmente coherentes para el procesamiento subsiguiente, denominado Xactsets. Un valor de **habilitado** significa que se puede crear Xactsets, que es el valor predeterminado. Un valor de **deshabilitado** significa que se procesa el Xactsets existentes por ningún nuevo Xactsets se crea.|  
|**xactsetjob**|Si el trabajo Xactset está habilitado para la creación de Xactsets. Un valor de **habilitado** significa que el trabajo Xactset se ejecuta periódicamente para crear Xactsets en el publicador. Un valor de **deshabilitado** significa que el Xactsets solo se crean mediante el agente de lector del registro cuando sondea el publicador buscando cambios.|  
|**xactsetjobinterval**|Intervalo entre ejecuciones del trabajo Xactset, en minutos.|  
  
 Cuando *propertyname* se omite se devuelven todas las propiedades configurables.  
  
 [**@propertyvalue** =] **'***propertyvalue***'**  
 Es el nuevo valor de la propiedad especificada. *PropertyValue* es **sysname**, su valor predeterminado es null. Cuando *propertyvalue* se omite, el valor actual de la propiedad se devuelve.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|Devuelve las siguientes propiedades de publicación que se pueden establecer:<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**PropertyValue**|**sysname**|Es el valor actual de la propiedad en el **propertyname** columna.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 **sp_publisherproperty** se utiliza en la replicación transaccional no es[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores.  
  
 Cuando solo *publisher* se especifica, el conjunto de resultados incluye la configuración actual para todas las propiedades que se pueden establecer.  
  
 Cuando *propertyname* se especifica, solo la propiedad con nombre aparece en el conjunto de resultados.  
  
 Cuando se especifican todos los parámetros, la propiedad se cambia y no se devuelve un conjunto de resultados.  
  
 Cuando se cambia el **xactsetjobinterval** propiedad para un trabajo en ejecución, debe reiniciar el trabajo para el nuevo intervalo surta efecto.  
  
## <a name="permissions"></a>Permissions  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor puede ejecutar **sp_publisherproperty**.  
  
## <a name="see-also"></a>Vea también  
 [Configuración del trabajo del conjunto de transacciones para un publicador de Oracle&#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
