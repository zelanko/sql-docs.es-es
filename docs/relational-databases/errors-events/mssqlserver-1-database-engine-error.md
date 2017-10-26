---
title: MSSQLSERVER_-1 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "-1"
helpviewer_keywords:
- -1 (Database Engine error)
ms.assetid: bad25b91-eaed-46c0-a5b7-71117a32304c
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d4ad7c2405b50c97e9d26f047089bc5069a3bc20
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver-1"></a>MSSQLSERVER_-1
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Identificador del evento|-1|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|Error al establecer una conexión al servidor.  Cuando se conecta con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o con versiones posteriores, la configuración predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite conexiones remotas. (Proveedor: interfaces de red SQL, error: 28 - El servidor no admite el protocolo requerido) (Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Error: -1)|  
  
## <a name="explanation"></a>Explicación  
El cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar al servidor. Este error podría deberse a uno de los siguientes motivos:  
  
-   El nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado no es válido.  
  
-   Los protocolos de canalizaciones con nombre o TCP no están habilitados.  
  
-   El firewall en el servidor ha rechazado la conexión.  
  
-   El servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser (sqlbrowser) no se inició.  
  
## <a name="user-action"></a>Acción del usuario  
Para resolver este error, intente una de las siguientes acciones:  
  
-   Compruebe la ortografía del nombre de instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se especifica en la cadena de conexión.  
  
-   Use la herramienta Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y aceptar las conexiones remotas a través de los protocolos de canalizaciones con nombre o TCP. Para obtener más información sobre cómo aceptar las conexiones remotas, vea [Habilitar o deshabilitar un protocolo de red de servidor](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md).  
  
-   Asegúrese de que ha configurado el firewall en la instancia de servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para abrir los puertos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el puerto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser (UDP 1434).  
  
-   Asegúrese de que el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser se inició en el servidor.  
  
## <a name="see-also"></a>Vea también  
[Configure a Windows Firewall for Database Engine Access](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) (Configurar Firewall de Windows para el acceso al motor de base de datos)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Protocolos de red y bibliotecas de red](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Configuración de red de cliente](~/database-engine/configure-windows/client-network-configuration.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Habilitar o deshabilitar un protocolo de red de servidor](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  

