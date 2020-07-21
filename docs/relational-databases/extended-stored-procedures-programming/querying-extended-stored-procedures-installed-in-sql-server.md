---
title: Consultar procedimientos almacenados extendidos
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 8413f071cfb36f5cad9130d3e2b56327d9b3bf45
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758096"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Consultar procedimientos almacenados extendidos instalados en SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuario autenticado puede mostrar los procedimientos almacenados extendidos definidos actualmente y el nombre de la dll a la que pertenece cada uno mediante la ejecución del procedimiento de sistema **sp_helpextendedproc** . Por ejemplo, en el ejemplo siguiente se devuelve el archivo DLL al que pertenece **xp_hello** :  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 Si se ejecuta **sp_helpextendedproc** sin especificar un procedimiento almacenado extendido, se muestran todos los procedimientos almacenados extendidos y sus dll.  
  
> [!IMPORTANT]  
>  Solamente se devolverá información para los procedimientos almacenados extendidos que posea el usuario o para los que tenga permisos. Solo los miembros del rol fijo de servidor **sysadmin** y de los roles fijos de base de datos **db_owner**, **db_securityadmin**y **db_ddladmin** pueden ver información de todos los procedimientos almacenados extendidos.  
  
## <a name="see-also"></a>Consulte también  
 [sp_helpextendedproc &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [sp_addextendedproc &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
