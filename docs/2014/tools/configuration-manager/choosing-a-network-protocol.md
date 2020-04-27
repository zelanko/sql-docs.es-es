---
title: Elección de un protocolo de red | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- shared memory [SQL Server]
- Named Pipes [SQL Server]
- TCP [SQL Server]
- network protocols [SQL Server], choosing
- protocols [SQL Server], choosing
- NWLink IPX/SPX [SQL Server]
- client configuration [SQL Server], protocols
- VIA
- Multiprotocol Net-Library [SQL Server]
- IPX/SPX [SQL Server]
- Banyan VINES
- protocols [SQL Server], client configuration
ms.assetid: 6565fb7d-b076-4447-be90-e10d0dec359a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 9c167994c7145bce348b6959a57533e398e1d6bb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63035294"
---
# <a name="choosing-a-network-protocol"></a>Elegir un protocolo de red
  Para conectarse a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] , debe tener habilitado un protocolo de red. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede atender solicitudes en varios protocolos al mismo tiempo. Los clientes se conectan a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un único protocolo. Si el programa cliente no sabe en qué protocolo escucha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , configure el cliente para intentar secuencialmente varios protocolos. Utilice el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar, deshabilitar y configurar protocolos de red.  
  
## <a name="shared-memory"></a>Memoria compartida  
 El protocolo de memoria compartida es el más sencillo de utilizar y no tiene ningún valor configurable. Dado que los clientes que utilizan el protocolo de memoria compartida solo se pueden conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecute en el mismo equipo, no es útil para la mayoría de las actividades de la base de datos. Utilice el protocolo de memoria compartida para la solución de problemas cuando sospeche que los demás protocolos no están configurados correctamente.  
  
> [!NOTE]  
>  Los clientes que utilizan MDAC 2.8 o versiones anteriores no pueden emplear el protocolo de memoria compartida. Si intentan hacerlo, se cambian automáticamente al protocolo Canalizaciones con nombre.  
  
## <a name="tcpip"></a>TCP/IP  
 TCP/IP es un protocolo habitual ampliamente utilizado en Internet. Se comunica a través de redes interconectadas de equipos que poseen diversas arquitecturas de hardware y distintos sistemas operativos. TCP/IP incluye estándares para enrutar el tráfico de red y ofrece características avanzadas de seguridad. Es el protocolo más popular empleado hoy en día. La configuración del equipo para usar TCP/IP puede ser compleja, pero la mayoría de los equipos en red ya están configurados correctamente. Para realizar la configuración TCP/IP que no está expuesta en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea la documentación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## <a name="named-pipes"></a>Canalizaciones con nombre  
 Canalizaciones con nombre es un protocolo desarrollado para redes de área local. Una parte de la memoria la usa un proceso para pasar información a otro, de modo que la salida de uno es la entrada del otro. El segundo proceso puede ser local (en el mismo equipo que el primero) o remoto (en un equipo en red).  
  
## <a name="named-pipes-vs-tcpip-sockets"></a>Canalizaciones con nombre frente a sockets TCP/IP  
 En un entorno LAN (Red de área local) rápido, los clientes de sockets TCP/IP (Protocolo de control de transporte/Protocolo de Internet) y las canalizaciones con nombre ofrecen un rendimiento similar. Sin embargo, la diferencia de rendimiento entre los clientes de Sockets TCP/IP y Canalizaciones con nombre se hace patente en redes lentas, por ejemplo a través de redes WAN (Red de área extensa) o redes de acceso telefónico. Esto se debe a las diferentes formas en que los mecanismos de comunicación entre procesos (IPC) se comunican entre nodos.  
  
 Para las canalizaciones con nombre, las comunicaciones de red suelen ser más interactivas. Un nodo no envía datos hasta que otro nodo los pide con un comando de lectura. Una lectura de red normalmente implica una serie de mensajes de canalizaciones con nombre de lectura antes de comenzar a leer los datos. Resultan muy costosos en una red lenta y causan un tráfico excesivo en la red, lo que, a su vez, afecta a otros clientes de la red.  
  
 También es importante aclarar si se trata de canalizaciones locales o canalizaciones de red. Si la aplicación servidor se ejecuta localmente en el equipo que ejecuta una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el protocolo de canalizaciones con nombre local es una opción. Las canalizaciones con nombre locales se ejecutan en modo de kernel y son muy rápidas.  
  
 Para los sockets TCP/IP, las transmisiones de datos son más precisas y tienen menos sobrecarga. Las transmisiones de datos también pueden aprovechar los mecanismos de mejora del rendimiento de los sockets TCP/IP, como ventanas, confirmación diferida, etc. Esto puede resultar muy beneficioso en una red lenta. Según el tipo de aplicaciones, estas diferencias de rendimiento pueden ser significativas.  
  
 Los sockets TCP/IP también aceptan una cola pendiente. Ésta puede proporcionar un efecto uniforme limitado si se compara con las canalizaciones con nombre, en las que puede obtener errores de canalización ocupada al intentar conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En general, se prefiere TCP/IP en una red LAN, WAN o de acceso telefónico lenta, mientras que las canalizaciones con nombre pueden ser una opción mejor cuando la velocidad de la red no es un problema, ya que ofrecen una mayor funcionalidad, y son más fáciles de usar y configurar.  
  
## <a name="enabling-the-protocol"></a>Habilitar el protocolo  
 Para que funcione, el protocolo debe estar habilitado en el cliente y el servidor. El servidor puede escuchar solicitudes en todos los protocolos habilitados al mismo tiempo. Los equipos cliente pueden elegir un protocolo o intentar usar los protocolos en el orden mostrado en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obtener un tutorial breve sobre cómo configurar protocolos y conectar al [!INCLUDE[ssDE](../../includes/ssde-md.md)], vea [Tutorial: Introducción al motor de base de datos](../../relational-databases/tutorial-getting-started-with-the-database-engine.md).  
  
  
