---
title: dbo.sysdownloadlist (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.sysdownloadlist
- sysdownloadlist_TSQL
- dbo.sysdownloadlist_TSQL
- sysdownloadlist
dev_langs:
- TSQL
helpviewer_keywords:
- sysdownloadlist system table
ms.assetid: 71087a4c-e829-488e-aa7d-a9476e2b4779
author: stevestein
ms.author: sstein
ms.openlocfilehash: 03e888cc3d36b909035247d5f1c16dd1ab61e0d3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061195"
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene la cola de instrucciones de descarga para todos los servidores de destino.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Columna de identidad que proporciona la secuencia de inserción natural de las filas.|  
|**source_server**|**sysname**|Nombre del servidor de origen.|  
|**operation_code**|**tinyint**|Código de operación del trabajo:<br /><br /> **1** = INS (INSERT)<br /><br /> **2** = UPD (ACTUALIZACIÓN)<br /><br /> **3** = SUPR (ELIMINAR)<br /><br /> **4** = INICIO<br /><br /> **5** = DETENER|  
|**object_type**|**tinyint**|Código de tipo de objeto.|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|Número de identificación del objeto.|  
|**target_server**|**sysname**|Nombre del servidor de destino.|  
|**error_message**|**nvarchar(1024)**|Mensaje de error si el servidor de destino encuentra un error al procesar la fila en particular.|  
|**date_posted**|**datetime**|Fecha y hora en que se envió el trabajo al servidor de destino.|  
|**date_downloaded**|**datetime**|Fecha y hora en que se descargó el trabajo por última vez.|  
|**status**|**tinyint**|Estado del trabajo:<br /><br /> **0** = no se ha descargado<br /><br /> **1** = descargado correctamente|  
|**deleted_object_name**|**sysname**|Nombre del objeto eliminado.|  
  
 <sup>1</sup> el **object_id** columna puede ser un valor de **-1**, que corresponde a un valor si todas las **operation_code** columna es un valor de eliminación.  
  
  
