---
title: PUBLISHINGSERVERNAME (Transact-SQL) | Documentos de Microsoft
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
- PUBLISHINGSERVERNAME_TSQL
- PUBLISHINGSERVERNAME
dev_langs:
- TSQL
helpviewer_keywords:
- PUBLISHINGSERVERNAME function
- Publishers [SQL Server replication], names
ms.assetid: e7c278e5-ab23-419e-ab3e-3bb20b0636df
caps.latest.revision: 16
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a5aeeb414f9c980429d20f123e1f9c986b147eee
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="replication-functions---publishingservername"></a>Funciones de replicación - PUBLISHINGSERVERNAME
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el nombre del publicador que publica una base de datos que participa en una sesión de creación de reflejo de la base de datos. Esta función se ejecuta en una instancia del publicador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la base de datos de publicaciones. Utilícela para determinar el publicador original de la base de datos publicada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
PUBLISHINGSERVERNAME()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **nvarchar**  
  
## <a name="remarks"></a>Comentarios  
 PUBLISHINGSERVERNAME se utiliza en todos los tipos de replicación.  
  
 PUBLISHINGSERVERNAME se utiliza cuando existe una sesión de creación de reflejo de la base de datos en la base de datos de publicaciones entre el publicador y una instancia asociada reflejada.  
  
 Esta función debe ejecutarse dentro del contexto de una base de datos de publicaciones. Cuando PUBLISHINGSERVERNAME se ejecuta en una base de datos de publicaciones en la instancia del servidor reflejado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se obtiene el nombre de la instancia del publicador desde el que se publica la base de datos. Cuando esta función se ejecuta en una base de datos en la instancia del servidor reflejado que no se ha publicado o que se ha publicado desde la misma tras una conmutación por error, se obtiene el nombre de esta instancia. Cuando esta función se ejecuta en la instancia del publicador original, se obtiene el nombre del publicador.  
  
## <a name="see-also"></a>Vea también  
 [Replicación y creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)   
 [Funciones de replicación &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/53702dee-de58-47d5-a552-7f32000f77d4)  
  
  

