---
title: Administrador de conexiones SMTP | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], SMTP
- SMTP connection manager [Integration Services]
- connection managers [Integration Services], SMTP
ms.assetid: 3795d442-714b-4bbb-9acd-75bf277a468a
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b05612ac34e4c2e7eb412d59eb9dcf5f28e99c78
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37213485"
---
# <a name="smtp-connection-manager"></a>Administrador de conexiones SMTP
  Un administrador de conexiones SMTP permite a un paquete conectarse a un servidor de Protocolo simple de transferencia de correo (SMTP). La tarea Enviar correo que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa un administrador de conexiones SMTP.  
  
 Si utiliza Microsoft Exchange como servidor SMTP, es posible que necesite configurar el administrador de conexiones SMTP para que utilice la autenticación de Windows. Es posible que los servidores Exchange estén configurados para no permitir conexiones SMTP no autenticadas.  
  
## <a name="configuration-the-smtp-connection-manager"></a>Configuración del administrador de conexiones SMTP  
 Cuando se agrega un administrador de conexiones SMTP a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una conexión de administrador que se resuelve como una conexión SMTP en tiempo de ejecución, Establece las propiedades del Administrador de la conexión y agrega el Administrador de conexiones para el `Connections` colección en el paquete. El `ConnectionManagerType` propiedad del Administrador de conexiones se establece en `SMTP`.  
  
 Puede configurar el administrador de conexiones SMTP de las maneras siguientes:  
  
-   Proporcionar una cadena de conexión.  
  
-   Especificar el nombre de un servidor SMTP.  
  
-   Especificar el método de autenticación que se va a utilizar.  
  
    > [!IMPORTANT]  
    >  El administrador de conexiones SMTP solo es compatible con la autenticación anónima y la autenticación de Windows. No admite la autenticación básica.  
  
-   Especificar si la comunicación se cifrará mediante SSL (Capa de sockets seguros) al enviar mensajes de correo electrónico.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que puede configurar en el Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor del administrador de conexiones SMTP](../smtp-connection-manager-editor.md).  
  
 Para obtener información acerca de cómo configurar un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [agregar conexiones mediante programación](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
