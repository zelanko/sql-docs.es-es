---
title: 'Protocolos de cliente: TCP y las propiedades IP (pestaña protocolo) | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- TCP/IP [SQL Server], client protocols
- client protocols [SQL Server]
ms.assetid: d04f1bce-069c-4a02-b561-c87c3282be36
caps.latest.revision: 24
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 2495b6c504083189313acf15e2bf8ecd0567aca2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199033"
---
# <a name="client-protocols---tcp-and-ip-properties-protocol-tab"></a>Protocolos de cliente: TCP y las propiedades IP (pestaña protocolo)
  En el Administrador de configuración de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use la pestaña **Protocolo** del cuadro de diálogo **Propiedades de TCP/IP** para ver o especificar las siguientes opciones. Para conectar a un puerto diferente, escriba el número de puerto en el cuadro **Puerto predeterminado** . Para obtener más información sobre cadenas de conexión, vea [Crear una cadena de conexión válida con TCP/IP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md).  
  
## <a name="options"></a>Opciones  
 **Puerto predeterminado**  
 Especifica el puerto que la biblioteca de red de TCP/IP utilizará para intentar conectarse a la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El puerto predeterminado es 1433.  
  
 Al conectar a una instancia predeterminada del [!INCLUDE[ssDE](../../includes/ssde-md.md)], el cliente utiliza este valor. Si se ha configurado una instancia predeterminada para que escuche en un puerto diferente, cambie este valor a dicho número de puerto.  
  
 Al conectar a una instancia con nombre del [!INCLUDE[ssDE](../../includes/ssde-md.md)], el cliente intentará obtener el número de puerto desde el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en el servidor. Si el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se está ejecutando, se debe proporcionar el número de puerto mediante esta configuración o como parte de la cadena de conexión.  
  
 **Enabled**  
 Los valores posibles son **Yes** y **No**.  
  
 **Keep Alive**  
 Este parámetro (en milisegundos) controla la frecuencia con la que TCP intenta comprobar que una conexión inactiva sigue intacta mediante el envío de un paquete **KEEPALIVE** . El valor predeterminado es 30000 milisegundos.  
  
 **Intervalo entre mensajes de mantenimiento de conexión**  
 Este parámetro (en milisegundos) determina el intervalo que separa las retransmisiones **KEEPALIVE** hasta que se recibe una respuesta. El valor predeterminado es 1000 milisegundos.  
  
## <a name="see-also"></a>Vea también  
 [Elegir un protocolo de red](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [Nuevo alias &#40;pestaña Alias&#41;](../../../2014/tools/configuration-manager/new-alias-alias-tab.md)   
 [&#60;Alias&#62; propiedades &#40;ficha Alias&#41;](../../../2014/tools/configuration-manager/alias-properties-alias-tab.md)  
  
  