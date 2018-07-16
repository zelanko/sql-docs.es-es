---
title: Quitar extendido procedimiento almacenado desde SQL Server | Microsoft Docs
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
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
caps.latest.revision: 36
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bacedfd7a485cf00b60992c1fd10d9f11b49ba89
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268941"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Quitar un procedimiento almacenado extendido de SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 Para quitar cada función de procedimiento almacenado extendido en un definido por el usuario extendido DLL de procedimiento almacenado un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrador del sistema debe ejecutar el **sp_dropextendedproc** especificando el nombre del procedimiento almacenado del sistema el función y el nombre del archivo DLL donde reside dicha función. Por ejemplo, este comando quita la función **xp_hello**, que se encuentra en un archivo DLL denominado xp_hello.dll, de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 A partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], **sp_dropextendedproc** no quita procedimientos almacenados extendidos del sistema. En su lugar, el administrador del sistema debe denegar el permiso EXECUTE en el procedimiento almacenado extendido a la **pública** rol.  
  
## <a name="see-also"></a>Vea también  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
