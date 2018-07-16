---
title: Propiedades de TCP / IP (pestaña de direcciones IP) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], listening on
- listening [SQL Server], on ports
ms.assetid: 4c17ed45-9da7-4bec-bce6-970109fe7365
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cb09573cd77f74044647925bd43310223c4ce67e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187601"
---
# <a name="tcp-ip-properties-ip-addresses-tab"></a>Propiedades de TCP / IP (pestaña de direcciones IP)
  Use el cuadro de diálogo **Propiedades de TCP/IP (pestaña Direcciones IP)** para configurar las opciones del protocolo TCP/IP para una dirección IP específica. Solo las opciones **Puertos dinámicos TCP** y **Puerto TCP** pueden configurarse para todas las direcciones al mismo tiempo seleccionando **IPAll**.  
  
 Los cambios surten efecto cuando se reinicia [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener información sobre cómo iniciar y detener el servicio SQL Server Browser, vea Cómo: Iniciar y detener el servicio SQL Server Browser en los libros en pantalla.  
  
## <a name="static-vs-dynamic-ports"></a>Puertos estáticos frente a Puertos dinámicos  
 La instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza escuchas para las conexiones entrantes en el puerto 1433. Se puede cambiar el puerto por razones de seguridad o debido a un requisito de la aplicación cliente. De forma predeterminada, las instancias con nombre (incluido SQL Server Express) se configuran para escuchar en los puertos dinámicos. Para configurar un puerto estático, deje en blanco la casilla **Puertos dinámicos TCP** y proporcione un número de puerto disponible en la casilla **Puerto TCP** . Para obtener más información acerca de cómo abrir los puertos del firewall, vea Configurar Firewall de Windows para permitir el acceso a SQL Server en los Libros en pantalla.  
  
## <a name="dynamic-ports"></a>Puertos dinámicos  
 Al iniciar, cuando una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está configurada para escuchar en puertos dinámicos, comprueba la existencia en el sistema operativo de un puerto disponible y abre un extremo para dicho puerto. Las conexiones entrantes deben especificar dicho número de puerto para conectarse. Puesto que el número de puerto puede cambiar cada vez que se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para supervisar los puertos y dirigir las conexiones entrantes al puerto actual para dicha instancia. El uso de puertos dinámicos dificulta la conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un firewall porque el número de puerto puede cambiar cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se reinicia, lo que implica tener que hacer cambios en la configuración del firewall. Para evitar problemas de conexión a través de un firewall, configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que utilice un puerto estático.  
  
## <a name="options"></a>Opciones  
 **Activo**  
 Indica que la dirección IP está activa en el equipo. No está disponible para **IPAll**.  
  
 **Enabled**  
 Si la propiedad **Escuchar todo** del cuadro de diálogo **Propiedades de TCP/IP (pestaña Protocolo)** se ha establecido en **No**, esta propiedad indicará si SQL Server está escuchando en la dirección IP. Si la propiedad **Escuchar todo** del cuadro de diálogo **Propiedades de TCP/IP (pestaña Protocolo)** se ha establecido en **Sí**, se omitirá esta propiedad. No está disponible para **IPAll**.  
  
 **Dirección IP**  
 Presenta o cambia la dirección IP empleada por esta conexión. Muestra la dirección IP empleada por el equipo y la dirección IP de bucle invertido, 127.0.0.1. No está disponible para **IPAll**. La dirección IP puede tener el formato IPv4 o IPv6.  
  
 **Puertos dinámicos TCP**  
 En blanco, si los puertos dinámicos no están habilitados. Para utilizar puertos dinámicos, establezca esta opción en 0.  
  
 Para **IPAll**, muestra el número del puerto dinámico utilizado.  
  
 **Puerto TCP**  
 Presenta o cambia el puerto en el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha. De manera predeterminada, la instancia predeterminada del [!INCLUDE[ssDE](../../includes/ssde-md.md)] escucha en el puerto 1433.  
  
 El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] puede escuchar en varios puertos con la misma dirección IP. Al enumerar los puertos, sepárelos con una coma siguiendo el formato 1433,1500,1501. Este campo tiene un límite de 2.047 caracteres.  
  
 Para configurar que una dirección IP única escuche en varios puertos, el parámetro **Escuchar todo** también se debe establecer en **No**, en la pestaña **Protocolos** del cuadro de diálogo **Propiedades de TCP/IP** . Para obtener más información, vea: "Cómo: Configurar el motor de base de datos para escuchar en varios puertos TCP" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="adding-or-removing-ip-addresses"></a>Agregar o quitar direcciones IP  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager muestra las direcciones IP que estaban disponibles en el momento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instaló. Las direcciones IP disponibles pueden cambiar cuando se agregan o se quitan tarjetas de red, cuando expira una dirección IP asignada dinámicamente, cuando se vuelve a configurar la estructura de red o cuando cambia la ubicación física del equipo, por ejemplo un equipo portátil que se conecta a la red en un edificio diferente. Para cambiar una dirección IP, edite el cuadro **Dirección IP** y, a continuación, reinicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Elegir un protocolo de red](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [Crear una cadena de conexión válida con TCP/IP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Servicio SQL Server Browser](../../../2014/tools/configuration-manager/sql-server-browser-service.md)  
  
  
