---
title: Quitar extendido procedimiento almacenado desde SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- deleting extended stored procedures
- removing extended stored procedures
- extended stored procedures [SQL Server], removing
- dropping extended stored procedures
ms.assetid: 7827e574-3f59-4279-9a9b-532582e041cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bcb58ac180861641803147d1dfea621bd52df9a6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62512030"
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
  
  
