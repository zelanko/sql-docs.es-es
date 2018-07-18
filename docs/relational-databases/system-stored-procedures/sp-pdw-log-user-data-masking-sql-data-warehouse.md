---
title: sp_pdw_log_user_data_masking (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-objects
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 16de9489583cce2e696a94c75c7e5fd3ac1c0fe1
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37993717"
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_log_user_data_masking** para habilitar el enmascaramiento de usuario en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad. Enmascaramiento de datos de usuario afecta a las instrucciones en todas las bases de datos en el dispositivo.  
  
> [!IMPORTANT]  
>  El [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad se ve afectado por **sp_pdw_log_user_data_masking** repítalas [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad. **sp_pdw_log_user_data_masking** no afecta a los registros de transacciones de base de datos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los registros de errores.  
  
 **En segundo plano:** en la configuración predeterminada [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad completo contienen [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones y puede que en algunos casos incluyen los datos contenidos en las operaciones, como **insertar**,  **ACTUALIZACIÓN**, y **seleccione** instrucciones. En el caso de un problema en el dispositivo, esto permite que el análisis de las condiciones que causó el problema sin necesidad de reproducir el problema. Con el fin de evitar que los datos de usuario que se escriben en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad, los clientes pueden elegir activar el enmascaramiento de datos de usuario mediante el uso de este procedimiento almacenado. Las instrucciones todavía se escribirán en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad, pero todos los literales de instrucciones que pueden contener datos de usuario se enmascarará; reemplazado con algunos valores constantes predefinidas.  
  
 Cuando se habilita el cifrado de datos transparente en el dispositivo, enmascaramiento de los datos de usuario [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad se activa automáticamente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>Parámetros  
 [  **@masking_mode=** ] *masking_mode*  
 Determina si está habilitados el enmascaramiento de datos del usuario de registro de cifrado transparente de los datos. *masking_mode* es **int**, y puede tener uno de los siguientes valores:  
  
-   0 = deshabilitado, los datos aparecen en el usuario la [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad.  
  
-   1 = habilitado, el usuario las instrucciones de datos aparecen en el [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] se enmascara los registros de actividad, pero los datos de usuario.  
  
-   2 = las instrucciones que contiene datos de usuario no se escriben en el [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad.  
  
 Ejecutar **sp_pdw_ log_user_data_masking** sin parámetros devuelve el estado actual del enmascaramiento de datos de usuario de registro TDE en el dispositivo como un conjunto de resultados escalares.  
  
## <a name="remarks"></a>Notas  
 Enmascaramiento de datos del usuario [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] habilita la sustitución de literales de registros de actividad con valores constantes predefinidos en **seleccione** y las instrucciones DML, ya que pueden contener datos de usuario. Establecer *masking_mode* a 1 no enmascara los metadatos, como nombres de columna o nombres de tabla. Establecer *masking_mode* para 2 ya no instrucciones con los metadatos, como nombres de columna o nombres de tabla.  
  
 Enmascaramiento de datos del usuario [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad se implementa en la siguiente manera:  
  
-   TDE y datos de usuario de enmascaramiento en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad están desactivados de forma predeterminada. Las instrucciones no se enmascara automáticamente si no está habilitado el cifrado de base de datos en el dispositivo.  
  
-   Habilitar TDE en el dispositivo automáticamente enciende el enmascaramiento de datos de usuario en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad.  
  
-   Deshabilitación de TDE no afecta a los datos de usuario de enmascaramiento en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad.  
  
-   Puede habilitar explícitamente los datos de usuario de enmascaramiento en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] los registros de actividad mediante el uso de la **sp_pdw_log_user_data_masking** procedimiento.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer a la **sysadmin** fijo de base de datos, o **CONTROL SERVER** permiso.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente habilita en el dispositivo de enmascaramiento de datos de usuario TDE registro.  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_pdw_database_encryption para &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
