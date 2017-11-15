---
title: "Propiedades de Agente SQL Server (página Conexión) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2d7cbddb41ee84f0525820980639de631b2033db
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="sql-server-agent-properties-connection-page"></a>Propiedades de Agente SQL Server (página Conexión)
Utilice esta página para ver y modificar la configuración de la conexión del servicio Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="options"></a>Opciones  
**Servidor de host local del alias**  
Especifica el alias que debe utilizarse para conectarse a la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Si no puede utilizar las opciones de conexión predeterminadas del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , defina un alias para la instancia y especifíquelo aquí.  
  
**Utilizar autenticación de Windows**  
Establece la autenticación de [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows como método de autenticación que se utiliza para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se conecta como la cuenta con la que se ejecuta el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
**Utilizar autenticación de SQL Server**  
Establece la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como método de autenticación que se utiliza para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se proporciona por motivos de compatibilidad con versiones anteriores. Para mejorar la seguridad, utilice la autenticación de Windows siempre que sea posible.  
  
**Inicio de sesión**  
Especifica el nombre de inicio de sesión que debe utilizarse para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
**Contraseña**  
Especifica la contraseña que debe utilizarse para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
