---
title: sp_pdw_database_encryption (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.service: sql-data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5f2c4fde17918e148ac26581fcb6f99057e38800
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86197318"
---
# <a name="sp_pdw_database_encryption-sql-data-warehouse"></a>sp_pdw_database_encryption (SQL Data Warehouse)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Use **sp_pdw_database_encryption** para habilitar el cifrado de datos transparente en para un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] dispositivo. Cuando **sp_pdw_database_encryption** establecida en 1, use la instrucción **ALTER DATABASE** para cifrar una base de datos mediante TDE.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>Parámetros  
`[ @enabled = ] enabled`Determina si está habilitado el cifrado de datos transparente. *Enabled* es de **tipo int**y puede tener uno de los valores siguientes:  
  
-   0 = Deshabilitado  
  
-   1 = Habilitado  
  
 Al ejecutar **sp_pdw_database_encryption** sin parámetros, se devuelve el estado actual de TDE en el dispositivo como un conjunto de resultados escalares: 0 para deshabilitado o 1 para habilitado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Observaciones  
 Cuando TDE se habilita mediante **sp_pdw_database_encryption**, la base de datos Tempdb se quita, se vuelve a crear y se cifra. Por ese motivo, el TDE no se puede habilitar en un dispositivo mientras haya otras sesiones activas mediante tempdb. La habilitación o deshabilitación de TDE en un dispositivo es una acción que cambia el estado del dispositivo, en la mayoría de los casos se espera que se realice una vez en la duración del dispositivo y que se ejecute cuando no haya tráfico en el dispositivo.  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de base de datos **sysadmin** o el permiso **Control Server** .  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se habilita TDE en el dispositivo.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
