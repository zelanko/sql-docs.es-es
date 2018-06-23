---
title: Crear una cadena de conexión válida con canalizaciones con nombre | Documentos de Microsoft
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
- connection strings [Database Engine], named pipes
- pipes [SQL Server]
- pipes [SQL Server], connecting to
- aliases [SQL Server], named pipes
- Named Pipes [SQL Server], connection strings
ms.assetid: 90930ff2-143b-4651-8ae3-297103600e4f
caps.latest.revision: 30
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 264c615e38baf39676f1310d6465bfaac2a92785
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107780"
---
# <a name="creating-a-valid-connection-string-using-named-pipes"></a>Crear una cadena de conexión válida con canalizaciones con nombre
  A menos que cambie por el usuario, cuando la instancia predeterminada de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escucha en el protocolo de canalizaciones con nombre, usa `\\.\pipe\sql\query` como el nombre de canalización. El punto indica que el equipo es el equipo local, `pipe` indica que la conexión es una canalización con nombre, y `sql\query` es el nombre de la canalización. Para conectarse a la canalización predeterminada, el alias debe incluir `\\<computer_name>\pipe\sql\query` como el nombre de canalización. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ha configurado para escuchar en una canalización diferente, el nombre de canalización debe utilizar esa canalización. Por ejemplo, si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza `\\.\pipe\unit\app` como canalización, el alias debe utilizar `\\<computer_name>\pipe\unit\app` como el nombre de canalización.  
  
 Para crear un nombre de canalización válido:  
  
-   Especifique un **Nombre de alias**.  
  
-   Seleccione **canalizaciones con nombre** como el **protocolo**.  
  
-   Escriba el **nombre de canalización**. Como alternativa, puede dejar **nombre de canalización** en blanco y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager se completará el nombre de canalización adecuada después de especificar el **protocolo** y **Server**  
  
-   Especifique un **Server**. Para una instancia con nombre, puede proporcionar un nombre de servidor y un nombre de instancia.  
  
 En el momento de la conexión, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componente Native Client lee el servidor, protocolo y nombre de la canalización valores del registro para el nombre de alias especificado y crea una canalización con nombre con el formato `np:\\<computer_name>\pipe\<pipename>` o `np:\\<IPAddress>\pipe\<pipename>`. Para una instancia con nombre, el nombre de canalización predeterminado es `\\<computer_name>\pipe\MSSQL$<instance_name>\sql\query`.  
  
> [!NOTE]  
>  La [!INCLUDE[msCoName](../../includes/msconame-md.md)] Firewall de Windows cierra el puerto 445 de forma predeterminada. Dado que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se comunica a través del puerto 445, debe volver a abrir el puerto si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se configura para escuchar conexiones de cliente entrantes mediante canalizaciones con nombre. Para obtener más información acerca de cómo configurar un firewall, vea “Cómo configurar un firewall para el acceso a SQL Server” en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o revise la documentación del firewall.  
  
## <a name="connecting-to-the-local-server"></a>Conectarse al servidor local  
 Al conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se ejecuta en el mismo equipo que el cliente, puede utilizar `(local)` como el nombre del servidor. El uso de `(local)` no se recomienda porque genera ambigüedad, pero puede ser útil cuando se sabe que el cliente se ejecuta en el equipo de destino. Por ejemplo, al crear una aplicación para usuarios desconectados móviles, como puede ser el personal de ventas, en la que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutará en equipos portátiles y se almacenarán datos de proyectos, un cliente que se conecte a (local) siempre se conectará al servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en el equipo portátil. En lugar de `localhost`, es posible usar `(local)` o un punto (.).  
  
## <a name="verifying-your-connection-protocol"></a>Comprobar el protocolo de conexión  
 La siguiente consulta devolverá el protocolo utilizado para la conexión actual.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>Ejemplos  
 Conectarse por el nombre de servidor a la canalización predeterminada:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 Conectarse por la dirección IP a la canalización predeterminada:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <leave blank>  
Protocol           Named Pipes  
Server             <IPAddress>  
  
```  
  
 Conectarse por el nombre de servidor a una canalización no predeterminada:  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\unit\app  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 Conectarse por el nombre de servidor a una instancia con nombre:  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\MSSQL$<instancename>\SQL\query  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 Conectarse al equipo local utilizando `localhost`:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             localhost  
  
```  
  
 Conectarse al equipo local utilizando un punto:  
  
```  
Alias Name         <serveralias>  
Pipe Name          <left blank>  
Protocol           Named Pipes  
Server             .  
  
```  
  
> [!NOTE]  
>  Para especificar el protocolo de red como un **sqlcmd** parámetro, consulte "Cómo: conectarse al motor de base de datos mediante sqlcmd.exe" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Crear una cadena de conexión válida con el protocolo de memoria compartida](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [Crear una cadena de conexión válida con TCP/IP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [Elegir un protocolo de red](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  