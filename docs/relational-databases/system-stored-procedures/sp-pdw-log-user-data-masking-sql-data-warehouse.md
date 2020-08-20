---
description: sp_pdw_log_user_data_masking (SQL Data Warehouse)
title: sp_pdw_log_user_data_masking (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 0857ffe4bae954efdbad4e1e692069a2b3eeab60
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473993"
---
# <a name="sp_pdw_log_user_data_masking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL Data Warehouse)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Use **sp_pdw_log_user_data_masking** para habilitar el enmascaramiento de datos del usuario en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad. El enmascaramiento de datos de usuario afecta a las instrucciones en todas las bases de datos del dispositivo.  
  
> [!IMPORTANT]  
>  Los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad afectados por **sp_pdw_log_user_data_masking** son determinados [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad. **sp_pdw_log_user_data_masking** no afecta a los registros de transacciones de la base de datos ni a los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registros de errores.  
  
 **Información general:** En, los registros de actividad de configuración predeterminados [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] contienen [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones completas y, en algunos casos, pueden incluir datos de usuario contenidos en operaciones como **Insert**, **Update**y **Select** . En caso de que se produzca un problema en el dispositivo, esto permite el análisis de las condiciones que han provocado el problema sin necesidad de reproducir el problema. Con el fin de evitar que los datos del usuario se escriban en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad, los clientes pueden optar por activar el enmascaramiento de datos del usuario mediante este procedimiento almacenado. Las instrucciones se seguirán escribiendo en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad, pero todos los literales de las instrucciones que pueden contener datos de usuario se enmascararán; se reemplazarán por algunos valores constantes predefinidos.  
  
 Cuando el cifrado de datos transparente está habilitado en el dispositivo, se activa automáticamente el enmascaramiento de los datos de usuario en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad.  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>Parámetros  
`[ @masking_mode = ] masking_mode` Determina si está habilitado el enmascaramiento de datos de usuario del registro de cifrado de datos transparente. *masking_mode* es de **tipo int**y puede tener uno de los valores siguientes:  
  
-   0 = deshabilitado, los datos de usuario aparecen en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad.  
  
-   1 = habilitada, las instrucciones de datos de usuario aparecen en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad, pero los datos del usuario se enmascaran.  
  
-   2 = las instrucciones que contienen datos de usuario no se escriben en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad.  
  
 Al ejecutar **sp_pdw_ log_user_data_masking** sin parámetros, se devuelve el estado actual del enmascaramiento de datos de usuario de registro de TDE en el dispositivo como un conjunto de resultados escalares.  
  
## <a name="remarks"></a>Observaciones  
 El enmascaramiento de datos de usuario en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad permite reemplazar literales con valores constantes predefinidos en instrucciones **Select** y DML, ya que pueden contener datos de usuario. Establecer *masking_mode* en 1 no enmascara metadatos, como nombres de columna o nombres de tabla. Si se establece *masking_mode* en 2, se quitan las instrucciones con metadatos, como nombres de columna o nombres de tabla.  
  
 El enmascaramiento de datos de usuario en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad se implementa de la siguiente manera:  
  
-   TDE y el enmascaramiento de datos de usuario en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad están desactivados de forma predeterminada. Las instrucciones no se enmascararán automáticamente si no está habilitado el cifrado de base de datos en el dispositivo.  
  
-   Al habilitar TDE en el dispositivo, se activa automáticamente el enmascaramiento de datos del usuario en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad.  
  
-   Deshabilitar TDE no afecta al enmascaramiento de datos de usuario en los [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad.  
  
-   Puede habilitar explícitamente el enmascaramiento de datos de usuario en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad mediante el procedimiento **sp_pdw_log_user_data_masking** .  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de base de datos **sysadmin** o el permiso **Control Server** .  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se habilita el enmascaramiento de datos de usuario de registro de TDE en el dispositivo.  
  
```sql  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_pdw_database_encryption &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
