---
description: sys.sysdevices (Transact-SQL)
title: Dispositivos sys.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysdevices
- sysdevices_TSQL
- sys.sysdevices
- sys.sysdevices_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysdevices compatibility view
- sysdevices system table
ms.assetid: ac5bcaf4-8fb6-4855-8856-d7643f469361
author: rothja
ms.author: jroth
ms.openlocfilehash: 6bcc481e595dc2c061d736a6bee12da6d918b7e8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419799"
---
# <a name="syssysdevices-transact-sql"></a>sys.sysdevices (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene una fila por cada archivo de copia de seguridad en disco, archivo de copia de seguridad en cinta y archivo de base de datos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre lógico del archivo de copia de seguridad o de base de datos.|  
|**size**|**int**|Tamaño del archivo en páginas de 2 KB.|  
|**habilita**|**int**|Se mantiene únicamente por compatibilidad con versiones anteriores.|  
|**calidad**|**int**|Se mantiene únicamente por compatibilidad con versiones anteriores.|  
|**status**|**smallint**|Mapa de bits que indica el tipo de dispositivo:<br /><br /> 1 = Disco predeterminado<br /><br /> 2 = Disco físico<br /><br /> 4 = Disco lógico<br /><br /> 8 = Omitir encabezado<br /><br /> 16 = Archivo de copia de seguridad<br /><br /> 32 = Escrituras en serie<br /><br /> 4096 = Solo lectura|  
|**cntrltype**|**smallint**|Tipo de controlador:<br /><br /> 0 = Archivo de base de datos que no está en CD-ROM<br /><br /> 2 = Archivo de copia de seguridad en disco<br /><br /> 3 - 4 = Archivo de copia de seguridad en disquete<br /><br /> 5 = Archivo de copia de seguridad en cinta<br /><br /> 6 = Archivo de canalización con nombre|  
|**phyname**|**nvarchar(260)**|Nombre del archivo físico.|  
  
## <a name="see-also"></a>Consulte también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
