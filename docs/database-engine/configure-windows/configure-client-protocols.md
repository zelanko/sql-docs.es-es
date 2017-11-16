---
title: Configurar protocolos de cliente | Microsoft Docs
ms.custom: 
ms.date: 07/27/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default protocols
- network protocols [SQL Server], client configuration
- TCP/IP [SQL Server], client protocols
- disabling client protocols
- ordering protocols [SQL Server]
- protocols [SQL Server], order for client computers
- configure client protocols
- client protocols [SQL Server]
- protocols [SQL Server], client configuration
- default protocols, client
ms.assetid: 3dfa2702-ba65-43b4-a777-6727846e133a
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 5cb93e598d20ad1622836579118d664c0e6da279
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="configure-client-protocols"></a>configurar protocolos de cliente
  En este tema se describe cómo configurar los protocolos de cliente utilizados por aplicaciones cliente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite comunicaciones de cliente con el protocolo de red TCP/IP y el protocolo de canalizaciones con nombre. El protocolo de memoria compartida también está disponible si el cliente se está conectando a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en el mismo equipo. Hay varios métodos habituales para seleccionar el protocolo.  
  
-   Configure todas las aplicaciones cliente para que usen el mismo protocolo de red estableciendo el orden de protocolos en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Configure una sola aplicación cliente para que use otro protocolo de red creando un alias. Para obtener más información, vea [Crear o eliminar un alias de servidor para que lo utilice un cliente &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md).  
  
-   Algunas aplicaciones cliente, como sqlcmd.exe, pueden especificar el protocolo como parte de la cadena de conexión. Para obtener más información, vea [Conectarse al motor de base de datos con sqlcmd](../../relational-databases/scripting/sqlcmd-connect-to-the-database-engine.md).  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
###  <a name="EnableDisable"></a> Para habilitar o deshabilitar un protocolo de cliente  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], expanda **Configuración de SQL Server Native Client**, haga clic con el botón derecho en **Protocolos de cliente** y, luego, haga clic en **Propiedades**.  
  
2.  Haga clic en un protocolo en el cuadro **Protocolos deshabilitados** y, a continuación, haga clic en **Habilitar**para habilitar el protocolo.  
  
3.  Haga clic en un protocolo en el cuadro **Protocolos habilitados** y, a continuación, haga clic en **Deshabilitar**para deshabilitar el protocolo.  
  
###  <a name="ChangeDefault"></a> Para cambiar el protocolo o el orden de protocolos predeterminado de los equipos cliente  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], expanda **Configuración de SQL Server Native Client**, haga clic con el botón derecho en **Protocolos de cliente** y, luego, haga clic en **Propiedades**.  
  
2.  En el cuadro **Protocolos habilitados** , haga clic en **Subir** o **Bajar**para cambiar el orden en el que los protocolos se utilizan cuando se intenta la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El protocolo superior del cuadro **Protocolos habilitados** es el protocolo predeterminado.  
  
    > [!IMPORTANT]  
    >  El Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea entradas del Registro para las configuraciones de alias del servidor y la biblioteca de red de cliente predeterminada. Sin embargo, la aplicación no instala ni las bibliotecas de red de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ni los protocolos de red. Las bibliotecas de red de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instalan durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; los protocolos de red se instalan como parte del programa de instalación de Microsoft Windows (o desde **Redes** en el **Panel de control**). Es posible que un protocolo de red específico no esté disponible como parte del programa de instalación de Windows. Para obtener más información acerca de cómo instalar estos protocolos de red, consulte la documentación del fabricante.  
  
###  <a name="Configure"></a> Para configurar el uso de TCP/IP en un cliente  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], expanda **Configuración de SQL Server Native Client**, haga clic con el botón derecho en **Protocolos de cliente** y, luego, haga clic en **Propiedades**.  
  
2.  En el cuadro **Protocolos habilitados** , haga clic en las flechas arriba o abajo para cambiar el orden en que se prueban los protocolos al intentar conectarse a SQL Server. El protocolo superior del cuadro **Protocolos habilitados** es el protocolo predeterminado.  
  
 El protocolo de memoria compartida se habilita de forma independiente activando la casilla **Habilitar el protocolo de memoria compartida** .  
  
## <a name="see-also"></a>Vea también  
 [Establecer la opción de configuración del servidor Tiempo de espera de inicio de sesión remoto](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)  
  
  
