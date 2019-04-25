---
title: Consultar procedimientos almacenados que se instala en SQL Server extendidos | Microsoft Docs
ms.custom: ''
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
manager: craigg
ms.openlocfilehash: f2d5584d70b32764fd9c7e11a53131626e9df444
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742231"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Consultar procedimientos almacenados extendidos instalados en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 Un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuario autenticado puede mostrar definido actualmente procedimientos almacenados extendidos y el nombre del archivo DLL para cada uno de ellos pertenece ejecutando el **sp_helpextendedproc** procedimiento del sistema. Por ejemplo, en el ejemplo siguiente se devuelve el archivo DLL en el cual **xp_hello** pertenece:  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 Si **sp_helpextendedproc** se ejecuta sin especificar un procedimiento almacenado extendido, los procedimientos almacenados extendidos y sus DLL se muestra.  
  
> [!IMPORTANT]  
>  Solamente se devolverá información para los procedimientos almacenados extendidos que posea el usuario o para los que tenga permisos. Solo los miembros de la **sysadmin** rol fijo de servidor y el **db_owner**, **db_securityadmin**y el **db_ddladmin** fijo de base de datos roles pueden ver información de todos los procedimientos almacenados extendidos.  
  
## <a name="see-also"></a>Vea también  
 [sp_helpextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
