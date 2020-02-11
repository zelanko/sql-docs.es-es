---
title: Quitar un procedimiento almacenado extendido de SQL Server | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62512030"
---
# <a name="removing-an-extended-stored-procedure-from-sql-server"></a>Quitar un procedimiento almacenado extendido de SQL Server
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]En su lugar, use la integración con CLR.  
  
 Para quitar cada función de procedimiento almacenado extendido en un archivo DLL de procedimiento almacenado extendido definido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el usuario, un administrador del sistema debe ejecutar el **sp_dropextendedproc** procedimiento almacenado del sistema, especificando el nombre de la función y el nombre del archivo dll en el que reside dicha función. Por ejemplo, este comando quita la función **xp_hello**, ubicada en un archivo dll denominado xp_hello. dll, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de:  
  
```  
sp_dropextendedproc 'xp_hello'  
```  
  
 A partir [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]de, **sp_dropextendedproc** no quita los procedimientos almacenados extendidos del sistema. En su lugar, el administrador del sistema debe denegar el permiso EXECUTe para el procedimiento almacenado extendido al rol **Public** .  
  
## <a name="see-also"></a>Consulte también  
 [sp_dropextendedproc &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql)  
  
  
