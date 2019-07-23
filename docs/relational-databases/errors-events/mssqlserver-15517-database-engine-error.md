---
title: MSSQLSERVER_15517 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15517 (Database Engine error)
ms.assetid: f94287f5-129f-4c52-9d34-62b996088001
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 88e0ab71648facd1f206e49870b04615949cf148
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100422"
---
# <a name="mssqlserver15517"></a>MSSQLSERVER_15517
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte también  
[OLTP en memoria &#40;optimización en memoria&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
