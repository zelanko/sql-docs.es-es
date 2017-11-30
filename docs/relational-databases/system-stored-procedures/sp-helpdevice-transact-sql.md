---
title: sp_helpdevice (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpdevice
- sp_helpdevice_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpdevice
ms.assetid: 1a5eafa7-384e-4691-ba05-978eb73bbefb
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a39dcc6cd75837017826fdcf9b37ff7d6a3598c9
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpdevice-transact-sql"></a>sp_helpdevice (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Proporciona información acerca de los dispositivos de copia de seguridad de Microsoft® SQL Server™.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Se recomienda que realice la [sys.backup_devices](../../relational-databases/system-catalog-views/sys-backup-devices-transact-sql.md) en su lugar de la vista de catálogo  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpdevice [ [ @devname = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@devname =** ] **'***nombre***'**  
 Es el nombre del dispositivo de copia de seguridad para el que se proporciona información. El valor de *nombre* siempre es **sysname**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**nombreDeDispositivo**|**sysname**|Nombre del dispositivo lógico.|  
|**argumento physical_name**|**nvarchar (260)**|Nombre de archivo físico.|  
|**Descripción**|**nvarchar(255)**|Descripción del dispositivo.|  
|**status**|**int**|Un número que corresponde a la descripción del estado de la **descripción** columna.|  
|**CntrlType**|**smallint**|Tipo de controlador del dispositivo:<br /><br /> 2 = Dispositivo de disco<br /><br /> 5 = Dispositivo de cinta|  
|**tamaño**|**int**|Tamaño del dispositivo en páginas de 2 KB.|  
  
## <a name="remarks"></a>Comentarios  
 Si *nombre* se especifica, **sp_helpdevice** muestra información sobre el dispositivo de volcado de memoria especificado. Si *nombre* no se especifica, **sp_helpdevice** muestra información acerca de todos los dispositivos de volcado de memoria en el **sys.backup_devices** vista de catálogo.  
  
 Dispositivos de volcado se agregan al sistema mediante **sp_addumpdevice**.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se proporciona información acerca de todos los dispositivos de volcado de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_helpdevice;  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_addumpdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [sp_dropdevice &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdevice-transact-sql.md)   
 [Motor de base de datos almacenados procedimientos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
