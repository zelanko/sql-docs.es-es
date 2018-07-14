---
title: sp_pdw_database_encryption para (SQL Data Warehouse) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.service: sql-data-warehouse
ms.component: system-objects
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 6508d150df663a6e95437d0b6b3bfd0c8f65906f
ms.sourcegitcommit: abd71294ebc39695d403e341c4f77829cb4166a8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/25/2018
ms.locfileid: "36926156"
---
# <a name="sppdwdatabaseencryption-sql-data-warehouse"></a>sp_pdw_database_encryption para (SQL Data Warehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_database_encryption para** para habilitar el cifrado de datos transparente para una [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] dispositivo. Cuando **sp_pdw_database_encryption para** establecido en 1, se utiliza el **ALTER DATABASE** instrucción para cifrar una base de datos mediante TDE.  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_pdw_database_encryption [ [ @enabled = ] enabled ] ;  
```  
  
#### <a name="parameters"></a>Parámetros  
 [  **@enabled=** ] *habilitado*  
 Determina si está habilitado el cifrado de datos transparente. *habilitado* es **int**, y puede tener uno de los siguientes valores:  
  
-   0 = Deshabilitado  
  
-   1 = Habilitado  
  
 Ejecutar **sp_pdw_database_encryption para** sin parámetros devuelve el estado actual de TDE en el dispositivo como un conjunto de resultados escalares: 0 para deshabilitado, o 1 para habilitado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Notas  
 Cuando está habilitado el TDE mediante **sp_pdw_database_encryption para**, se quita la base de datos tempdb, se vuelve a crear y cifrado. Por ese motivo, el TDE no se puede habilitar un dispositivo mientras hay otras sesiones activas con tempdb. Habilitación o deshabilitación de TDE en un dispositivo es una acción que cambia el estado del dispositivo, en la mayoría de los casos se espera que se puede realizar una vez en la duración de la aplicación y se debe ejecutar cuando no hay ningún tráfico en el dispositivo.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer a la **sysadmin** fijo de base de datos, o **CONTROL SERVER** permiso.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo siguiente habilita TDE en el dispositivo.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
