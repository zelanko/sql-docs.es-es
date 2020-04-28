---
title: Quitar un procedimiento almacenado extendido
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.custom: seo-dt-2019
ms.openlocfilehash: ec61cf630d606977689d3fb3763cce8bd8b705c8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74095433"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Quitar un procedimiento almacenado extendido de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 Para quitar cada función de procedimiento almacenado extendido en un archivo DLL de procedimiento almacenado extendido definido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el usuario, un administrador del sistema debe ejecutar el **sp_dropextendedproc** procedimiento almacenado del sistema, especificando el nombre de la función y el nombre del archivo dll en el que reside dicha función. Por ejemplo, este comando quita la función **xp_hello**, ubicada en un archivo dll denominado xp_hello. dll, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 A partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]de, **sp_dropextendedproc** no quita los procedimientos almacenados extendidos del sistema. En su lugar, el administrador del sistema debe denegar el permiso EXECUTe para el procedimiento almacenado extendido al rol **Public** .  
  
## <a name="see-also"></a>Consulte también  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)  
  
  
