---
title: Descargar una DLL de procedimiento almacenado extendido | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2772c8d6470f9ad6eb5e8b7cadb6dedd136bd48b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63137582"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Descargar una DLL de procedimiento almacenado extendido
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]En su lugar, use la integración con CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carga una DLL de procedimiento almacenado extendido en cuanto se realiza una llamada a una de las funciones del archivo dll. La DLL sigue cargada hasta que se cierra el servidor o hasta que el administrador del sistema utiliza la instrucción DBCC para descargarla. Por ejemplo, este comando descarga la **xp_hello. dll**, lo que permite al administrador del sistema copiar una versión más reciente de este archivo en el directorio sin apagar el servidor:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Consulte también  
 [DBCC DllName &#40;FREE&#41; &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dllname-free-transact-sql)  
  
  
