---
title: Descargar una DLL de procedimiento almacenado extendido | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
ms.openlocfilehash: 76007876547b863f050d1e3fa494cbd8b30a5fc0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85717659"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Descargar una DLL de procedimiento almacenado extendido
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]carga una DLL de procedimiento almacenado extendido en cuanto se realiza una llamada a una de las funciones del archivo dll. La DLL sigue cargada hasta que se cierra el servidor o hasta que el administrador del sistema utiliza la instrucción DBCC para descargarla. Por ejemplo, este comando descarga el **xp_hello.dll**, lo que permite al administrador del sistema copiar una versión más reciente de este archivo en el directorio sin apagar el servidor:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Consulte también  
 [DBCC DllName &#40;FREE&#41; &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)  
  
  
