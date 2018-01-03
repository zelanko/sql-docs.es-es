---
title: managed_backup.sp_backup_on_demand (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs: TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
caps.latest.revision: "13"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 539b5c0bba5597f872f1a651701dcf325ca9d8e2
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="managedbackupspbackupondemand-transact-sql"></a>managed_backup.sp_backup_on_demand (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Solicita [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] que realice una copia de seguridad de la base de datos especificada.  
  
 Utilice este procedimiento almacenado para realizar copias de seguridad ad hoc para una base de datos configurada con [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Esto evita la interrupción en la cadena de copias de seguridad, los procesos de [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] lo saben y la copia de seguridad se almacena en el mismo contenedor de almacenamiento Blob de Windows Azure.  
  
 Tras finalizar correctamente la copia de seguridad, se devuelve la ruta de acceso al archivo de la copia de seguridad completa. Esto incluye el nombre y la ubicación del nuevo archivo de copia de seguridad resultante de la operación de copia de seguridad.  
  
 Se devuelve un error si [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] está en el proceso de ejecutar una copia de seguridad de un tipo determinado para la base de datos especificada. En este caso, el mensaje de error devuelto incluye la ruta de acceso al archivo de copia de seguridad completa donde la copia de seguridad actual se carga.  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @database_name  
 El nombre de la base de datos en la que se realiza la copia de seguridad. El @database_name es **SYSNAME**.  
  
 @type  
 Tipo de la copia de seguridad que se va a realizar: base de datos o registro. El @type parámetro es **nvarchar (32)**.  
  
## <a name="return-code-value"></a>Valor de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere la pertenencia a **db_backupoperator** rol, la base de datos con **ALTER ANY CREDENTIAL** permisos, y **EXECUTE** permisos **sp_delete_ backuphistory**procedimiento almacenado.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se realiza una solicitud de copia de seguridad de base de datos para la base de datos ‘TestDB’. Esta base de datos tiene [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] habilitado.  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 Para cada fragmento de código, seleccione 'tsql' en el campo de atributo language.  
  
  
