---
title: '@@PACK_RECEIVED (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@PACK_RECEIVED_TSQL'
- '@@PACK_RECEIVED'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@PACK_RECEIVED function'
- number of packets read
- packets [SQL Server], number read
ms.assetid: 5c0b3d36-bfad-4f0b-abb8-e8f6391b32cd
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a4d0bfea159c945dab24060144783221513e9fcd
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="x40x40packreceived-transact-sql"></a>& #x 40; & #x 40; PACK_RECEIVED (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de paquetes de entrada leídos desde la red por parte de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde que se inició por última vez.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@PACK_RECEIVED  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **integer**  
  
## <a name="remarks"></a>Comentarios  
 Para mostrar un informe que contenga varias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estadísticas, incluidos los paquetes enviados y recibidos, ejecutan **sp_monitor**.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se muestra el uso de `@@PACK_RECEIVED`.  
  
```  
SELECT @@PACK_RECEIVED AS 'Packets Received';   
```  
  
 A continuación se muestra un conjunto de resultados de ejemplo.  
  
```  
Packets Received  
----------------  
128  
```  
  
## <a name="see-also"></a>Vea también  
 [@@PACK_SENT](../../t-sql/functions/pack-sent-transact-sql.md)   
 [sp_monitor](../../relational-databases/system-stored-procedures/sp-monitor-transact-sql.md)   
 [Funciones estadísticas del sistema](../../t-sql/functions/system-statistical-functions-transact-sql.md)  
  
  

