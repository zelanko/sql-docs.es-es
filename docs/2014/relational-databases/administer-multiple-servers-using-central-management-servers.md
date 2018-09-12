---
title: Administrar varios servidores mediante Servidores de administración central | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
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
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: efc9759ffdc64361986a1e0285051afb9bb1290e
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43810821"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>Administrar varios servidores mediante Servidores de administración central
  Puede administrar varios servidores designando los servidores de administración central y creando grupos de servidores.  
  
## <a name="benefits-of-central-management-servers-and-server-groups"></a>Ventajas de los servidores de administración central y grupos de servidores  
 Una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que se designa como servidor de administración central mantiene los grupos de servidores que contienen la información de conexión de una o varias instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Las instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] y las directivas de la administración basada en directivas se pueden ejecutar al mismo tiempo con grupos de servidores. También puede ver los archivos de registro de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en las instancias que se administran a través de un Servidor de administración central. Las versiones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] no se pueden designar como Servidores de administración central.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] también se pueden ejecutar con los grupos de servidores locales en Servidores registrados.  
  
### <a name="related-tasks"></a>Related Tasks  
 Para crear un Servidor de administración central y grupos de servidores, use la ventana **Servidores registrados** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Observe que el servidor de administración central no puede ser miembro de un grupo que mantenga. Para obtener más información sobre cómo crear servidores de administración central y grupos de servidores, vea [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md).  
  
## <a name="see-also"></a>Vea también  
 [Administrar servidores mediante administración basada en directivas](policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
