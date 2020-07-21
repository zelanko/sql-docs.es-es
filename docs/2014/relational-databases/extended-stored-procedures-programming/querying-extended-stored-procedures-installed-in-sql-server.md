---
title: Consultar procedimientos almacenados extendidos instalados en SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f44db9053ad18c3a6902a30aaab4f81610c5a8c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050834"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Consultar procedimientos almacenados extendidos instalados en SQL Server
    
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
 [sp_helpextendedproc &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql)   
 [sp_addextendedproc &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
