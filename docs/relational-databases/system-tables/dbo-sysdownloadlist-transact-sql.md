---
description: dbo.sysdownloadlist (Transact-SQL)
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 0240d13b1f787eb9b0356b1443f8401477176d0a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446673"
---
# <a name="dbosysdownloadlist-transact-sql"></a>dbo.sysdownloadlist (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contiene la cola de instrucciones de descarga para todos los servidores de destino.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**instance_id**|**int**|Columna de identidad que proporciona la secuencia de inserción natural de las filas.|  
|**source_server**|**sysname**|Nombre del servidor de origen.|  
|**operation_code**|**tinyint**|Código de operación del trabajo:<br /><br /> **1** = ins (Insert)<br /><br /> **2** = UPD (actualizar)<br /><br /> **3** = Supr (eliminar)<br /><br /> **4** = Inicio<br /><br /> **5** = detener|  
|**object_type**|**tinyint**|Código de tipo de objeto.|  
|**object_id** <sup>1</sup>|**uniqueidentifier**|Número de identificación del objeto.|  
|**target_server**|**sysname**|Nombre del servidor de destino.|  
|**error_message**|**nvarchar(1024)**|Mensaje de error si el servidor de destino encuentra un error al procesar la fila en particular.|  
|**date_posted**|**datetime**|Fecha y hora en que se envió el trabajo al servidor de destino.|  
|**date_downloaded**|**datetime**|Fecha y hora en que se descargó el trabajo por última vez.|  
|**status**|**tinyint**|Estado del trabajo:<br /><br /> **0** = sin descargar aún<br /><br /> **1** = descargado correctamente|  
|**deleted_object_name**|**sysname**|Nombre del objeto eliminado.|  
  
 <sup>1</sup> la columna de **object_id** puede tener un valor de **-1**, que corresponde a un valor de All si la **operation_code** columna es un valor de DELETE.  
  
  
