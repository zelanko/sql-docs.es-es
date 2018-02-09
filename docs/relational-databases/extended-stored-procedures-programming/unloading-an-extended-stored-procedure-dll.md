---
title: Descargar extendido DLL de procedimiento almacenado | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: extended-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3bad1f82152cd21d4d5753225842b672016ccec2
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Descargar una DLL de procedimiento almacenado extendido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, use la integración con CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]carga un archivo DLL de procedimiento almacenado extendido en cuanto se realiza una llamada a una de las funciones del archivo DLL. La DLL sigue cargada hasta que se cierra el servidor o hasta que el administrador del sistema utiliza la instrucción DBCC para descargarla. Por ejemplo, este comando descarga el **xp_hello.dll**, al permitir al administrador del sistema copiar una versión más reciente de este archivo en el directorio sin necesidad de apagar el servidor:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Vea también  
 [DBCC dllname &#40;FREE&#41; &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
