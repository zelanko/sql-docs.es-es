---
title: Quitar un extendido el procedimiento almacenado de SQL Server | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: extended-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
caps.latest.revision: 37
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3086ddb460e71ec890abf26e982e83a696c5fe0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Quitar un procedimiento almacenado extendido de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 Para quitar cada función de procedimiento almacenado extendido en un definido por el usuario extendido DLL de procedimiento almacenado un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrador del sistema debe ejecutar el **sp_dropextendedproc** especifica el nombre del procedimiento almacenado del sistema el función y el nombre de la DLL en el que reside dicha función. Por ejemplo, este comando quita la función **xp_hello**, que se encuentra en un archivo DLL denominado xp_hello.dll, de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **sp_dropextendedproc** no quita procedimientos almacenados extendido del sistema. En su lugar, el administrador del sistema debe denegar el permiso EXECUTE en el procedimiento almacenado extendido a la **público** rol.  
  
## <a name="see-also"></a>Vea también  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
