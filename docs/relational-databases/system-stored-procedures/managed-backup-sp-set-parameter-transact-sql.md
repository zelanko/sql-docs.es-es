---
title: managed_backup. sp_set_parameter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_set_parameter_TSQL
- sp_set_parameter
- smart_admin.sp_set_parameter
- smart_admin.sp_set_parameter_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_parameter
- smart_admin.sp_set_parameter
ms.assetid: bd8ae5fd-1337-4b7f-b0a4-153cbca9fa5f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 3eab417e1d959c990e53aca3119546a73a3e1aad
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052921"
---
# <a name="managed_backupsp_set_parameter-transact-sql"></a>managed_backup. sp_set_parameter (Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  Establece el valor del parámetro del sistema de Administración inteligente especificado.  
  
 Los parámetros disponibles se relacionan con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Estos parámetros se utilizan para establecer las notificaciones por correo electrónico, habilitar eventos extendidos específicos y habilitar directivas de administración basada en directivas de conjunto de usuarios. Debe especificar los pares de valores del parámetro y el nombre del parámetro.  

  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
EXEC managed_backup.sp_set_parameter   
    [@parameter_name = ] {'SSMBackup2WANotificationEmailIds' | 'SSMBackup2WAEnableUserDefinedPolicy' | 'SSMBackup2WADebugXevent' | 'FileRetentionDebugXevent' | 'StorageOperationDebugXevent'}  
    ,[@parameter_value = ] 'parameter_value'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>Argumentos  
 @parameter_name  
 Nombre del parámetro para el que desea establecer el valor. @parameter_namees de tipo NVARCHAR (128). Los nombres de parámetro disponibles son **SSMBackup2WANotificationEmailIds**, **SSMBackup2WADebugXevent**, **SSMBackup2WAEnableUserDefinedPolicy**, **FileRetentionDebugXevent**y **StorageOperationDebugXevent**.  
  
 @parameter_value  
 Valor del parámetro que desea establecer. @parameterel valor es NVARCHAR (128).  Los siguientes son pares permitidos de nombre de parámetro y valor:  
  
-   @parameter_name= ' SSMBackup2WANotificationEmailIds ': @parameter_value = ' email '  
  
-   @parameter_name= ' SSMBackup2WAEnableUserDefinedPolicy ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name= ' SSMBackup2WADebugXevent ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name= ' FileRetentionDebugXevent ': @parameter_value = {' true ' | ' false '}  
  
-   @parameter_name= ' StorageOperationDebugXevent ' = {' true ' | ' false '}  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="best-practices"></a>Prácticas recomendadas  
 Sección opcional que describe las prácticas recomendadas que el usuario debe conocer al ejecutar la instrucción o la rutina.  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 Requiere permisos **Execute** en **managed_backup. sp_set_parameter** procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes habilitan los eventos extendidos operativos y de depuración.  
  
```  
-- to enable operational events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionOperationalXevent', 'True'  
--  to enable debug events  
Use msdb;  
Go  
         EXEC managed_backup.sp_set_parameter 'FileRetentionDebugXevent', 'True'  
  
```  
  
 El ejemplo siguiente habilita las notificaciones por correo electrónico de los errores y advertencias y establece el emailID que se usa para enviar las notificaciones:  
  
```  
Use msdb  
Go  
EXEC managed_backup.sp_set_parameter @parameter_name = 'SSMBackup2WANotificationEmailIds', @parameter_value = '<email address>'  
  
```  
  
  
