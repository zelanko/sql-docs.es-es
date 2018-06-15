---
title: sp_pdw_log_user_data_masking (almacenamiento de datos de SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: data-warehouse
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 43c63b42-03cb-4fb5-8362-ec3b7e22a590
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6b158d6c0ea65159d6e310512ee45abb4916a0e7
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
ms.locfileid: "33701825"
---
# <a name="sppdwloguserdatamasking-sql-data-warehouse"></a>sp_pdw_log_user_data_masking (almacenamiento de datos de SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_log_user_data_masking** para permitir que los datos de usuario de enmascaramiento en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad. El enmascaramiento de datos de usuario afecta a las instrucciones en todas las bases de datos en el dispositivo.  
  
> [!IMPORTANT]  
>  El [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad se ve afectado por **sp_pdw_log_user_data_masking** está seguro de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad. **sp_pdw_log_user_data_masking** no afecta a los registros de transacciones de base de datos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registros de errores.  
  
 **En segundo plano:** en la configuración predeterminada [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad contienen completa [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones y puede que en algunos casos incluyen datos de usuario contenidos en operaciones como **insertar**,  **ACTUALIZACIÓN**, y **seleccione** instrucciones. En el caso de un problema en el dispositivo, esto permite que el análisis de las condiciones que ha causado el problema sin necesidad de reproducir el problema. Para evitar que los datos de usuario que se escriben en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad, los clientes pueden elegir activar el enmascaramiento de datos de usuario mediante el uso de este procedimiento almacenado. Las instrucciones todavía se escribirán en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad, pero todos los literales de instrucciones que pueden contener datos de usuario se enmascare; reemplazado con algunos valores de constantes predefinidas.  
  
 Cuando se habilita el cifrado de datos transparente en el dispositivo, el enmascaramiento de los datos de usuario [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad se activa automáticamente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_log_user_data_masking [ [ @masking_mode = ] value ] ;  
```  
  
#### <a name="parameters"></a>Parámetros  
 [  **@masking_mode=** ] *masking_mode*  
 Determina si está habilitados el enmascaramiento de datos del usuario de registro de cifrado transparente de los datos. *masking_mode* es **int**, y puede tener uno de los siguientes valores:  
  
-   0 = deshabilitado, el usuario que los datos aparecen en la [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad.  
  
-   1 = Enabled, usuario instrucciones de datos aparecen en la [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad, pero los datos de usuario se enmascara.  
  
-   2 = las instrucciones que contienen datos de usuario no se escriben en el [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad.  
  
 Ejecutar **sp_pdw_ log_user_data_masking** sin parámetros, se devuelve el estado actual del enmascaramiento de datos de usuario de registro TDE en el dispositivo como un conjunto de resultados escalares.  
  
## <a name="remarks"></a>Comentarios  
 Datos de usuario de enmascaramiento en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] habilita la sustitución de literales de registros de actividad con los valores de constantes predefinidos en **seleccione** y las instrucciones DML, ya que pueden contener datos de usuario. Establecer *masking_mode* en 1 no enmascara los metadatos, como nombres de columna o nombres de tabla. Establecer *masking_mode* a 2 quita las instrucciones con los metadatos, como nombres de columna o nombres de tabla.  
  
 Datos de usuario de enmascaramiento en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad se implementa de la siguiente manera:  
  
-   TDE y datos de usuario de enmascaramiento en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad están desactivados de forma predeterminada. Las instrucciones no se enmascara automáticamente si no está habilitado el cifrado de base de datos en el dispositivo.  
  
-   Habilitar TDE en el dispositivo automáticamente activará el enmascaramiento de datos de usuario en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad.  
  
-   Deshabilitación de TDE no afecta a los datos de usuario de enmascaramiento en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad.  
  
-   Puede habilitar explícitamente los datos de usuario de enmascaramiento en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] registros de actividad mediante el uso de la **sp_pdw_log_user_data_masking** procedimiento.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **sysadmin** función fija de base de datos, o **CONTROL SERVER** permiso.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se habilita en el dispositivo de enmascaramiento de datos de usuario TDE registro.  
  
```  
EXEC sp_pdw_log_user_data_masking 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_pdw_database_encryption &#40;almacenamiento de datos SQL&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)   
 [sp_pdw_database_encryption_regenerate_system_keys &#40;almacenamiento de datos SQL&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
  
