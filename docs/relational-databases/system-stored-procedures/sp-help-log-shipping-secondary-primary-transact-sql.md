---
title: sp_help_log_shipping_secondary_primary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_log_shipping_secondary_primary
- sp_help_log_shipping_secondary_primary_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_log_shipping_secondary_primary
ms.assetid: 1310fdaf-edb5-4294-9739-7fb37c2c2cb5
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7aaa40e2542c3010e697e370cd4124982b35d41e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85893627"
---
# <a name="sp_help_log_shipping_secondary_primary-transact-sql"></a>sp_help_log_shipping_secondary_primary (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Este procedimiento almacenado recupera la configuración de una base de datos principal determinada en el servidor secundario.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_log_shipping_secondary_primary  
[ @primary_server = ] 'primary_server' OR  
[ @primary_database = ] 'primary_database'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @primary_server = ] 'primary_server'`Nombre de la instancia principal de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en la configuración del trasvase de registros. *primary_server* es de **tipo sysname** y no puede ser null.  
  
`[ @primary_database = ] 'primary_database'`Es el nombre de la base de datos del servidor principal. *primary_database* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 El **conjunto de resultados**contiene las columnas **secondary_id**, **primary_server**, **primary_database**, **backup_source_directory**, **backup_destination_directory**, **file_retention_period**, **copy_job_id**, restore_job_id **,** monitor_server **monitor_server_security_mode log_shipping_secondary.** **restore_job_id**  
  
## <a name="remarks"></a>Comentarios  
 **sp_help_log_shipping_secondary_primary** se debe ejecutar desde la base de datos **maestra** en el servidor secundario.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar este procedimiento.  
  
## <a name="see-also"></a>Consulte también  
 [Acerca del trasvase de registros &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
