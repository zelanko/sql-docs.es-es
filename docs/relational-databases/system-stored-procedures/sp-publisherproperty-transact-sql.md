---
title: sp_publisherproperty (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 37b94b68702394b73ae810b246c0701e876802de
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43023258"
---
# <a name="sppublisherproperty-transact-sql"></a>sp_publisherproperty (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Muestra o cambia las propiedades de publicadores que no sean de[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores. Este procedimiento almacenado se ejecuta en el distribuidor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_publisherproperty [ @publisher = ] 'publisher'   
   [ , [ @propertyname = ] 'propertyname' ]   
   [ , [ @propertyvalue = ] 'propertyvalue' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [**@publisher** =] **'***publisher***'**  
 Es el nombre del publicador heterogéneo. *publicador* es **sysname**, no tiene ningún valor predeterminado.  
  
 [**@propertyname** =] **'***propertyname***'**  
 Es el nombre de la propiedad que se va a establecer. *PropertyName* es **sysname**, y puede tener uno de los siguientes valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**xactsetbatching**|Si las transacciones en el publicador están agrupadas en conjuntos transaccionalmente coherentes para el procesamiento subsiguiente, denominado Xactsets. Un valor de **habilitado** significa que Xactsets se puede crear, que es el valor predeterminado. Un valor de **deshabilitado** significa que se procesa el Xactsets existentes por ningún nuevo Xactsets se crea.|  
|**xactsetjob**|Si el trabajo Xactset está habilitado para la creación de Xactsets. Un valor de **habilitado** significa que el trabajo Xactset se ejecuta periódicamente para crear Xactsets en el publicador. Un valor de **deshabilitado** significa que el Xactsets solo se crean mediante el registro del log cuando sondea el publicador buscando cambios.|  
|**xactsetjobinterval**|Intervalo entre ejecuciones del trabajo Xactset, en minutos.|  
  
 Cuando *propertyname* se omite se devuelven todas las propiedades configurables.  
  
 [**@propertyvalue** =] **'***propertyvalue***'**  
 Es el nuevo valor de la propiedad especificada. *PropertyValue* es **sysname**, su valor predeterminado es null. Cuando *propertyvalue* se omite, el valor actual de la propiedad se devuelve.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**propertyname**|**sysname**|Devuelve las siguientes propiedades de publicación que se pueden establecer:<br /><br /> **xactsetbatching**<br /><br /> **xactsetjob**<br /><br /> **xactsetjobinterval**|  
|**PropertyValue**|**sysname**|Es el valor actual de la propiedad en el **propertyname** columna.|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 **sp_publisherproperty** se utiliza en la replicación transaccional para que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores.  
  
 Cuando solo *publisher* se especifica, el conjunto de resultados incluye la configuración actual de todas las propiedades que se pueden establecer.  
  
 Cuando *propertyname* se especifica, solo la propiedad con nombre aparece en el conjunto de resultados.  
  
 Cuando se especifican todos los parámetros, la propiedad se cambia y no se devuelve un conjunto de resultados.  
  
 Al cambiar el **xactsetjobinterval** propiedad para un trabajo en ejecución, debe reiniciar el trabajo para el nuevo intervalo surta efecto.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor en el distribuidor puede ejecutar **sp_publisherproperty**.  
  
## <a name="see-also"></a>Vea también  
 [Configuración del trabajo del conjunto de transacciones para un publicador de Oracle&#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
