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
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 039646f41ae952d21cca7047b0942aa8bcf10860
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Descargar una DLL de procedimiento almacenado extendido
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carga un archivo DLL de procedimiento almacenado extendido en cuanto se realiza una llamada a una de las funciones del archivo DLL. La DLL sigue cargada hasta que se cierra el servidor o hasta que el administrador del sistema utiliza la instrucción DBCC para descargarla. Por ejemplo, este comando descarga el **xp_hello.dll**, al permitir al administrador del sistema copiar una versión más reciente de este archivo en el directorio sin necesidad de apagar el servidor:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Vea también  
 [Nombre de DLL DBCC &#40; LIBRE &#41; &#40; Transact-SQL &#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
