---
title: Descargar extendido DLL de procedimiento almacenado | Documentos de Microsoft
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
- extended stored procedures [SQL Server], unloading
- unloading extended stored procedures
ms.assetid: 4c75ab14-af54-4965-b376-8d75d385c941
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 78d3e74d7316b31143253a2c1bd7c33d08b012f2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197385"
---
# <a name="unloading-an-extended-stored-procedure-dll"></a>Descargar una DLL de procedimiento almacenado extendido
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] En su lugar, utilice la integración con CLR.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carga un archivo DLL de procedimiento almacenado extendido en cuanto se realiza una llamada a una de las funciones del archivo DLL. La DLL sigue cargada hasta que se cierra el servidor o hasta que el administrador del sistema utiliza la instrucción DBCC para descargarla. Por ejemplo, este comando descarga el **xp_hello.dll**, al permitir al administrador del sistema copiar una versión más reciente de este archivo en el directorio sin necesidad de apagar el servidor:  
  
```  
DBCC xp_hello(FREE)  
```  
  
## <a name="see-also"></a>Vea también  
 [Nombre de DLL DBCC &#40;libre&#41; &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dllname-free-transact-sql)  
  
  
