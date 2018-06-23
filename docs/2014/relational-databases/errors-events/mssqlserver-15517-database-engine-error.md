---
title: MSSQLSERVER_15517 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
caps.latest.revision: 5
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 06e21c4e075dbf092e4ae3731b38806390ea2a47
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104248"
---
# <a name="mssqlserver15517"></a>MSSQLSERVER_15517
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|15517|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SEC_CANNOTEXECUTEASUSER|  
|Texto del mensaje|No se puede ejecutar como la entidad de seguridad de base de datos porque la entidad "*entidad*" no existe, este tipo de entidad de seguridad no se puede suplantar o el usuario no tiene permiso.|  
  
## <a name="user-action"></a>Acción del usuario  
 Use el nombre de una entidad de seguridad existente u obtenga el permiso IMPERSONATE para esa entidad de seguridad.  
  
 También puede producirse el evento 15517 después de que alguien que no sea el propietario de la base de datos original adjunte y restaure una base de datos. Para resolver este error, cambie el db_owner a un inicio de sesión en el servidor mediante el comando siguiente:  
  
```  
ALTER AUTHORIZATION ON DATABASE:: DBName TO [NewLogin]  
```  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  