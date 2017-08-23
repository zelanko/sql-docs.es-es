---
title: "Protocolos de cliente: propiedades de TCP / IP (pestaña protocolo) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- TCP/IP [SQL Server], client protocols
- client protocols [SQL Server]
ms.assetid: d04f1bce-069c-4a02-b561-c87c3282be36
caps.latest.revision: 25
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c9f7f7beee862cbb257ac4c6d117e11ecec0af5b
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# Protocolos de cliente: Propiedades de TCP/IP (pestaña Protocolo)
  En el Administrador de configuración de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use la pestaña **Protocolo** del cuadro de diálogo **Propiedades de TCP/IP** para ver o especificar las siguientes opciones. Para conectar a un puerto diferente, escriba el número de puerto en el cuadro **Puerto predeterminado** . Para obtener más información sobre cadenas de conexión, vea [Crear una cadena de conexión válida con TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md).  
  
## Opciones  
 **Puerto predeterminado**  
 Especifica el puerto que la biblioteca de red de TCP/IP utilizará para intentar conectarse a la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El puerto predeterminado es 1433.  
  
 Al conectar a una instancia predeterminada del [!INCLUDE[ssDE](../../includes/ssde-md.md)], el cliente utiliza este valor. Si se ha configurado una instancia predeterminada para que escuche en un puerto diferente, cambie este valor a dicho número de puerto.  
  
 Al conectar a una instancia con nombre del [!INCLUDE[ssDE](../../includes/ssde-md.md)], el cliente intentará obtener el número de puerto desde el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en el servidor. Si el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se está ejecutando, se debe proporcionar el número de puerto mediante esta configuración o como parte de la cadena de conexión.  
  
 **Habilitado**  
 Los valores posibles son **Yes** y **No**.  
  
 **Keep Alive**  
 Este parámetro (en milisegundos) controla la frecuencia con la que TCP intenta comprobar que una conexión inactiva sigue intacta mediante el envío de un paquete **KEEPALIVE** . El valor predeterminado es 30000 milisegundos.  
  
 **Intervalo entre mensajes de mantenimiento de conexión**  
 Este parámetro (en milisegundos) determina el intervalo que separa las retransmisiones **KEEPALIVE** hasta que se recibe una respuesta. El valor predeterminado es 1000 milisegundos.  
  
## Vea también  
 [Elegir un protocolo de red](http://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)   
 [Nuevo Alias &#40; Ficha alias &#41;](../../tools/configuration-manager/new-alias-alias-tab.md)   
 [Propiedades de &#60;Alias&#62; &#40;pestaña Alias&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md)  
  
  
