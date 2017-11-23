---
title: dbo.sysdownloadlist (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dbo.sysdownloadlist
- sysdownloadlist_TSQL
- dbo.sysdownloadlist_TSQL
- sysdownloadlist
dev_langs: TSQL
helpviewer_keywords: sysdownloadlist system table
ms.assetid: 71087a4c-e829-488e-aa7d-a9476e2b4779
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64ab3c661ff3cb5aa92d11e8193680629af9851b
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene la cola de instrucciones de descarga para todos los servidores de destino.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**valor de instance_id**|**int**|Columna de identidad que proporciona la secuencia de inserción natural de las filas.|  
|**Source_server**|**sysname**|Nombre del servidor de origen.|  
|**operation_code**|**tinyint**|Código de operación del trabajo:<br /><br /> **1** = INS (INSERT)<br /><br /> **2** = UPD (ACTUALIZACIÓN)<br /><br /> **3** = SUPR (ELIMINAR)<br /><br /> **4** = INICIO<br /><br /> **5** = DETENER|  
|**object_type**|**tinyint**|Código de tipo de objeto.|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|Número de identificación del objeto.|  
|**target_server**|**sysname**|Nombre del servidor de destino.|  
|**error_message**|**nvarchar (1024)**|Mensaje de error si el servidor de destino encuentra un error al procesar la fila en particular.|  
|**date_posted**|**datetime**|Fecha y hora en que se envió el trabajo al servidor de destino.|  
|**date_downloaded**|**datetime**|Fecha y hora en que se descargó el trabajo por última vez.|  
|**status**|**tinyint**|Estado del trabajo:<br /><br /> **0** = no se ha descargado<br /><br /> **1** = descargado correctamente|  
|**deleted_object_name**|**sysname**|Nombre del objeto eliminado.|  
  
 <sup>1</sup> el **object_id** columna puede ser un valor de **-1**, que corresponde a un valor de ALL si la **operation_code** columna es un valor de eliminación.  
  
  
