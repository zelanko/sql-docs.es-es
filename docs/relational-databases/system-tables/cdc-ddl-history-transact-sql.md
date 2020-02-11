---
title: CDC. ddl_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.ddl_history_TSQL
- cdc.ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.ddl_history
ms.assetid: cb97ea71-da2f-441a-bbd2-db1f5f48ab49
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1855120dde6e6f4e9037a6f14832cd24f310d77b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079223"
---
# <a name="cdcddl_history-transact-sql"></a>cdc.ddl_history (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada cambio del lenguaje de definición de datos (DDL) realizado en las tablas que se habilitan para la captura de datos de cambio. Puede utilizar esta tabla para determinar cuándo tuvo lugar un cambio de DDL en una tabla de origen y el contenido del cambio. Las tablas de origen que no tenían cambios de DDL no tendrán entradas en esta tabla.  
  
 Se recomienda que no consulte directamente las tablas del sistema. En su lugar, ejecute el procedimiento almacenado [Sys. sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) .  
   
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**source_object_id**|**int**|Id. de la tabla de origen al que se aplicó el cambio de DDL.|  
|**object_id**|**int**|Id. de la tabla de cambio asociado con una instancia de captura para la tabla de origen.|  
|**required_column_update**|**bit**|Indica que el tipo de datos de una columna capturada se modificó en la tabla de origen. Esta modificación alteró la columna en la tabla de cambio.|  
|**ddl_command**|**nvarchar(max)**|Instrucción DDL aplicada a la tabla de origen.|  
|**ddl_lsn**|**binario (10)**|Número de secuencia de registro (LSN) asociado con la confirmación de la modificación de DDL.|  
|**ddl_time**|**datetime**|Fecha y hora en la que se realizó el cambio de DDL en la tabla de origen.|  
  
## <a name="see-also"></a>Consulte también  
 [Sys. sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [CDC. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
