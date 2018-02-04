---
title: sp_pdw_database_encryption (almacenamiento de datos de SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: 
ms.service: sql-data-warehouse
ms.component: system-stored-procedures
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: f5ccb424-7a95-4557-b774-c69de33c1545
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8e63022bd135d7c5fc78dd717b6a0bdd27dc5311
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sppdwdatabaseencryption-sql-data-warehouse"></a>sp_pdw_database_encryption (almacenamiento de datos de SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Use **sp_pdw_database_encryption** para habilitar el cifrado de datos transparente en un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] dispositivo. Cuando **sp_pdw_database_encryption** establecido en 1, se utiliza el **ALTER DATABASE** instrucción para cifrar una base de datos mediante TDE.  
  
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
  
 Ejecutar **sp_pdw_database_encryption** sin parámetros, se devuelve el estado actual de TDE en el dispositivo como un conjunto de resultados escalares: 0 para deshabilitado, o 1 para habilitado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Cuando el TDE está habilitado con **sp_pdw_database_encryption**, se quita la base de datos tempdb, se vuelven a crear y cifrado. Por esta razón, no puede habilitarse TDE en un dispositivo mientras hay otras sesiones activas con tempdb. Habilitación o deshabilitación de TDE en una aplicación es una acción que cambia el estado del dispositivo, en la mayoría de los casos se espera que se realice una vez en la duración de la aplicación y debe ejecutarse cuando no hay ningún tipo de tráfico en el dispositivo.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **sysadmin** función fija de base de datos, o **CONTROL SERVER** permiso.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se habilita TDE en el dispositivo.  
  
```sql  
EXEC sys.sp_pdw_database_encryption 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)   
 [sp_pdw_log_user_data_masking &#40;SQL Data Warehouse&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
  
