---
title: Sys. syslogins (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syslogins_TSQL
- syslogins
- sys.syslogins
- sys.syslogins_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.syslogins compatibility view
- syslogins system table
ms.assetid: 4cb34f17-a4bb-469f-a218-71f074e6308f
author: rothja
ms.author: jroth
ms.openlocfilehash: 5745d3f98741d4a414c7bb69d8f9865258d47e34
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020009"
---
# <a name="syssyslogins-transact-sql"></a>sys.syslogins (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada cuenta de inicio de sesión.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta la [versión actual](https://go.microsoft.com/fwlink/p/?LinkId=299658)).  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Junction**|**varbinary(85)**|Identificador de seguridad.|  
|**estatus**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**CreateDate**|**datetime**|Fecha en que se agregó el inicio de sesión.|  
|**updatedate**|**datetime**|Fecha en que se actualizó el inicio de sesión.|  
|**accdate**|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totcpu**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**totio**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**spacelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**timelimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**resultlimit**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Name**|**sysname**|Nombre de inicio de sesión del usuario.|  
|**nombrebd**|**sysname**|Nombre de la base de datos predeterminada del usuario al establecer una conexión.|  
|**contraseña**|**nvarchar(128)**|Devuelve NULL.|  
|**módulo**|**sysname**|Idioma predeterminado del usuario.|  
|**denylogin**|**int**|1 = El inicio de sesión corresponde a un usuario o grupo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows al que se le ha denegado el acceso.|  
|**hasaccess**|**int**|1 = El inicio de sesión tiene acceso al servidor.|  
|**isntname**|**int**|1 = El inicio de sesión corresponde a un usuario o grupo de Windows.<br /><br /> 0 = Es un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**isntgroup**|**int**|1 = El inicio de sesión corresponde a un grupo de Windows.|  
|**isntuser**|**int**|1 = El inicio de sesión corresponde a un usuario de Windows.|  
|**sysadmin**|**int**|1 = el inicio de sesión es miembro del rol de servidor **sysadmin** .|  
|**securityadmin**|**int**|1 = el inicio de sesión es miembro del rol de servidor **securityadmin** .|  
|**ServerAdmin**|**int**|1 = el inicio de sesión es miembro del rol fijo de servidor **ServerAdmin** .|  
|**setupadmin**|**int**|1 = el inicio de sesión es miembro del rol fijo de servidor **setupadmin** .|  
|**processadmin**|**int**|1 = el inicio de sesión es miembro del rol fijo de servidor **processadmin** .|  
|**diskadmin**|**int**|1 = el inicio de sesión es miembro del rol fijo de servidor **diskadmin** .|  
|**dbcreator**|**int**|1 = el inicio de sesión es miembro del rol fijo de servidor **dbcreator** .|  
|**bulkadmin**|**int**|1 = el inicio de sesión es miembro del rol fijo de servidor **bulkadmin** .|  
|**LoginName**|**nvarchar(128)**|Nombre de inicio de sesión del usuario. Se proporciona para mantener la compatibilidad con versiones anteriores.|  
  
## <a name="see-also"></a>Consulte también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
