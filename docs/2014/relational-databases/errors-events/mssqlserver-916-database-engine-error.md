---
title: MSSQLSERVER_916 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 916 (Database Engine error)
ms.assetid: 73eb6581-99fe-49a5-9b42-e239d7ffe27f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eed360e125d387a85c225833957f80fdb72c07b6
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86550790"
---
# <a name="mssqlserver_916"></a>MSSQLSERVER_916
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|916|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NOTUSER|  
|Texto del mensaje|La entidad de seguridad de servidor "%.*ls" no puede tener acceso a la base de datos "%.\*ls" en el contexto de seguridad actual.|  
  
## <a name="explanation"></a>Explicación  
 El inicio de sesión no tiene los permisos suficientes para conectar a la base de datos denominada. Los inicios de sesión que se puedan conectar a esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero que no tengan los permisos correspondientes en una base de datos, reciben los permisos del usuario guest. Se trata de una medida de seguridad para evitar que los usuarios de una base de datos se conecten a otras en las que no tienen privilegios. Este mensaje de error se puede producir cuando el usuario guest no dispone del permiso CONNECT para la base de datos denominada y no se ha establecido la propiedad TRUSTWORTHY. Este mensaje de error se puede producir cuando el usuario guest no dispone del permiso CONNECT para la base de datos denominada.  
  
 Cuando se deniega o revoca el permiso CONNECT para la base de datos msdb, es posible que [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] reciba este error si el Explorador de objetos intenta mostrar el estado de la administración basada en directivas de cada base de datos. El Explorador de objetos se sirve de los permisos del inicio de sesión actual para realizar consultas sobre esta información a la base de datos msdb, lo cual produce el error. También se produce el siguiente mensaje de error:  
  
 Error al recuperar datos para esta solicitud. (Microsoft.SqlServer.Management.Sdk.Sfc)  
  
## <a name="user-action"></a>Acción del usuario  
  
> [!WARNING]  
>  Antes de sortear esta medida de seguridad, asegúrese de que comprende perfectamente qué significa que los usuarios se autentiquen en varias bases de datos. Los siguientes métodos pueden permitir a los usuarios con permisos en una base de datos conectarse a otras, lo cual podría exponer los datos a usuarios malintencionados. Cuando se habilitan las bases de datos independientes, los siguientes pasos permiten a los propietarios de una base de datos conceder acceso a la otra base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Puede conectarse a la base de datos mediante uno de los siguientes procedimientos:  
  
-   Otorgue el acceso de inicio de sesión específico a la base de datos denominada. En el siguiente ejemplo se concede el inicio de sesión para el acceso de `Adventure-Works\Larry` a la base de datos `msdb`.  
  
     USE msdb ;  
  
     GO  
  
     GRANT CONNECT TO [Adventure-Works\Larry] ;  
  
-   Otorgue el permiso CONNECT a la base de datos denominada en el mensaje de error del usuario guest. En el siguiente ejemplo se concede el permiso `CONNECT` para la base de datos `msdb` al usuario `guest`.  
  
     USE msdb ;  
  
     GO  
  
     GRANT CONNECT TO guest ;  
  
-   Habilite la propiedad TRUSTWORTHY en la base de datos que ha autenticado al usuario.  
  
     `ALTER DATABASE AdventureWorks SET TRUSTWORTHY ON;`  
  
  
