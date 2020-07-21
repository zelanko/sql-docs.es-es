---
title: DBCC dllname (FREE) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- dbcc_dllname_(FREE)_TSQL
- dllname
- dbcc dllname (FREE)
- FREE
- dbcc_dllname(FREE)_TSQL
- FREE_TSQL
- dllname_TSQL
- dbcc dllname(FREE)
dev_langs:
- TSQL
helpviewer_keywords:
- DLL unloading [SQL Server]
- DBCC dllname (FREE)
- freeing DLLs
- unloading DLLs
ms.assetid: 1eb71c17-fe15-430b-8916-e4e312dcf9c0
author: pmasl
ms.author: umajay
ms.openlocfilehash: aeac2877165b3d0b00d33fd62e8e81086d951f0b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85894882"
---
# <a name="dbcc-dllname-free-transact-sql"></a>DBCC dllname (FREE) (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
Descarga de la memoria la DLL del procedimiento almacenado extendido especificado.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
```sql
DBCC <dllname> ( FREE ) [ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>Argumentos  
 \<*dllname*>  
 Es el nombre de la biblioteca DLL que se va a descargar de la memoria.  
  
 WITH NO_INFOMSGS  
 Suprime todos los mensajes de información.  
  
## <a name="remarks"></a>Observaciones
Cuando se ejecuta un procedimiento almacenado extendido, la DLL permanece cargada por la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hasta que se cierra el servidor. Esta instrucción permite que se pueda descargar de la memoria una DLL sin tener que cerrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para mostrar los archivos DLL cargados actualmente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ejecute **sp_helpextendedproc**.
  
## <a name="result-sets"></a>Conjuntos de resultados  
Si se especifica una DLL válida, DBCC *dllname* (FREE) devuelve:
  
```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permisos  
Debe pertenecer al rol fijo de servidor **sysadmin** o al rol fijo de base de datos **db_owner** .
  
## <a name="examples"></a>Ejemplos  
En el siguiente ejemplo se da por supuesto que `xp_sample` se ha implementado como xp_sample.dll y se ha ejecutado. DBCC \<*dllname*> (FREE) descarga el archivo xp_sample.dll asociado al procedimiento extendido `xp_sample`.
  
```sql  
DBCC xp_sample (FREE);  
```  
  
## <a name="see-also"></a>Consulte también  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[Características de ejecución de los procedimientos almacenados extendidos](../../relational-databases/extended-stored-procedures-programming/execution-characteristics-of-extended-stored-procedures.md)  
[sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)  
[sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
[sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)  
[Descargar una DLL de procedimiento almacenado extendido](../../relational-databases/extended-stored-procedures-programming/unloading-an-extended-stored-procedure-dll.md)
  
  
