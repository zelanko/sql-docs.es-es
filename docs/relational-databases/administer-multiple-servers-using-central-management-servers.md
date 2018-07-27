---
title: Administrar varios servidores mediante Servidores de administración central | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: relational-databases-misc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
caps.latest.revision: 27
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2a6c9b1e58b09e81eee64c471af9b6c562521f4
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082367"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>Administrar varios servidores mediante Servidores de administración central
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Puede administrar varios servidores designando los servidores de administración central y creando grupos de servidores.  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>¿Qué son un servidor de administración central y los grupos de servidores?  
 Una instancia de SQL Server designada como servidor de administración central mantiene los grupos de servidores que contienen la información de conexión de una o varias instancias. Puede ejecutar instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] y directivas de administración basada en directivas al mismo tiempo en grupos de servidores. También puede ver los archivos de registro en las instancias que se administran a través de un servidor de administración central. 
 
 Básicamente, un servidor de administración central es un repositorio central que contiene una lista de los servidores administrados. Las versiones anteriores a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] no se pueden designar como servidores de administración central.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] también se pueden ejecutar con los grupos de servidores locales en Servidores registrados.  
  
## <a name="create-central-management-server-and-server-groups"></a>Crear servidor de administración central y grupos de servidores 
 Para crear un Servidor de administración central y grupos de servidores, use la ventana **Servidores registrados** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Observe que el servidor de administración central no puede ser miembro de un grupo que mantenga. 
 
 Para obtener más información sobre cómo crear servidores de administración central y grupos de servidores, consulte [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  
  
## <a name="see-also"></a>Vea también  
 [Administrar servidores mediante administración basada en directivas](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
