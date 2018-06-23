---
title: Consultar procedimientos almacenados que se instala en SQL Server extendidos | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], querying
ms.assetid: e02348e6-dba6-438a-98b6-684244bb034d
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 25e9b8d1de6acd52182e090f40d955cc17bf5cd1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202499"
---
# <a name="querying-extended-stored-procedures-installed-in-sql-server"></a>Consultar procedimientos almacenados extendidos instalados en SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use la integración con CLR en su lugar.  
  
 A [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuario autenticado puede mostrar las personalizaciones definidas actualmente procedimientos almacenados extendidos y el nombre de la DLL a la que cada pertenece mediante la ejecución de la **sp_helpextendedproc** procedimiento del sistema. Por ejemplo, en el ejemplo siguiente se devuelve el archivo DLL en el cual **xp_hello** pertenece:  
  
```  
sp_helpextendedproc 'xp_hello'  
```  
  
 Si **sp_helpextendedproc** se ejecuta sin especificar un procedimiento almacenado extendido, los procedimientos almacenados extendidos y sus archivos DLL se muestran.  
  
> [!IMPORTANT]  
>  Solamente se devolverá información para los procedimientos almacenados extendidos que posea el usuario o para los que tenga permisos. Solo los miembros de la **sysadmin** rol fijo de servidor y el **db_owner**, **db_securityadmin**y el **db_ddladmin** fijo de base de datos roles pueden ver información de todos los procedimientos almacenados extendidos.  
  
## <a name="see-also"></a>Vea también  
 [sp_helpextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql)   
 [sp_addextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
