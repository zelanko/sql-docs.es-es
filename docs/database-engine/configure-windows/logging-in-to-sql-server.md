---
title: "Iniciar una sesión en SQL Server | Microsoft Docs"
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
- SQL Server, logging in
- services [SQL Server], logging in
- TCP connection string
- connecting to the Database Engine
- logins [SQL Server], about logging in
- named pipe connection string
- log ins [SQL Server]
- shared memory connection string
- logging in [SQL Server]
- logins [SQL Server]
ms.assetid: 77158a9a-d638-4818-90a1-cb2eb57df514
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b4ed2e0c35921a717fc9447e62d469fb0153a74c
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="logging-in-to-sql-server"></a>Iniciar una sesión en SQL Server
  Puede iniciar una sesión en una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con cualquiera de las herramientas gráficas de administración o desde el símbolo del sistema.  
  
 Cuando se inicia una sesión en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante una herramienta gráfica de administración, como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], el sistema pedirá el nombre del servidor, un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y una contraseña, si es necesario. Si inicia una sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando la autenticación de Windows, no tendrá que proporcionar un inicio de sesión de SQL Server cada vez que tenga acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En su lugar, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza su cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para iniciar la sesión automáticamente. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta con autenticación de modo mixto (modo de autenticación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y de Windows) y decide iniciar una sesión mediante la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe proporcionar un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y una contraseña. Siempre que sea posible, utilice la autenticación de Windows.  
  
> [!NOTE]  
>  Si al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]seleccionó una intercalación que distingue entre mayúsculas y minúsculas, el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también distinguirá entre mayúsculas y minúsculas.  
  
## <a name="format-for-specifying-the-name-of-sql-server"></a>Formato para especificar el nombre de SQL Server  
 Al conectar a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe especificar el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es la instancia predeterminada (una instancia sin nombre), especifique el nombre del equipo donde está instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o la dirección IP del equipo. Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es una instancia con nombre (como SQLEXPRESS), especifique el nombre del equipo donde está instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o la dirección IP del equipo, y agregue una barra diagonal y el nombre de instancia.  
  
 Los ejemplos siguientes se conectan a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en un equipo denominado APPHOST. Al especificar una instancia con nombre, los ejemplos usan un nombre de instancia SQLEXPRESS.  
  
 **Ejemplos:**  
  
|Tipo de instancia|Entrada para el nombre de servidor|  
|----------------------|-------------------------------|  
|Conexión a una instancia predeterminada mediante el protocolo predeterminado. (Esta es la entrada recomendada para una instancia predeterminada).|APPHOST|  
|Conexión a una instancia con nombre mediante el protocolo predeterminado. (Esta es la entrada recomendada para una instancia con nombre.)|APPHOST\SQLEXPRESS|  
|Conexión a una instancia predeterminada en el mismo equipo con un punto para indicar que la instancia se está ejecutando en el equipo local.|.|  
|Conexión a una instancia con nombre en el mismo equipo con un punto para indicar que la instancia se está ejecutando en el equipo local.|.\SQLEXPRESS|  
|Conexión a una instancia predeterminada en el mismo equipo con localhost para indicar que la instancia se está ejecutando en el equipo local.|localhost|  
|Conexión a una instancia con nombre en el mismo equipo con localhost para indicar que la instancia se está ejecutando en el equipo local.|localhost\SQLEXPRESS|  
|Conexión a una instancia predeterminada en el mismo equipo con (local) para indicar que la instancia se está ejecutando en el equipo local.|(local)|  
|Conexión a una instancia con nombre en el mismo equipo con (local) para indicar que la instancia se está ejecutando en el equipo local.|(local)\SQLEXPRESS|  
|Conexión a una instancia predeterminada en el mismo equipo que fuerza una conexión de memoria compartida.|lpc:APPHOST|  
|Conexión a una instancia con nombre en el mismo equipo que fuerza una conexión de memoria compartida.|lpc:APPHOST\SQLEXPRESS|  
|Conexión a una instancia predeterminada que escucha en la dirección TCP 192.168.17.28 con una dirección IP.|192.168.17.28|  
|Conexión a una instancia con nombre que escucha en la dirección TCP 192.168.17.28 con una dirección IP.|192.168.17.28\SQLEXPRESS|  
|Conexión a una instancia predeterminada que no escucha en el puerto TCP, mediante la especificación del puerto que se está usando, en este caso 2828. (Esto no es necesario si [!INCLUDE[ssDE](../../includes/ssde-md.md)] escucha en el puerto predeterminado (1433)).|APPHOST,2828|  
|Conexión a una instancia con nombre en un puerto TCP designado, en este caso 2828. (Esto suele ser necesario si el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser no se está ejecutando en el equipo host.)|APPHOST,2828|  
|Conexión a una instancia predeterminada que no escucha en el puerto TCP, mediante la especificación tanto de la dirección IP como del puerto TCP que se está usando, en este caso 2828.|192.168.17.28,2828|  
|Conexión a una instancia con nombre mediante la especificación tanto de la dirección IP como del puerto TCP que se está usando, en este caso 2828.|192.168.17.28,2828|  
|Conexión a una instancia predeterminada por nombre, lo que fuerza una conexión TCP.|tcp:APPHOST|  
|Conexión a una instancia con nombre por nombre, lo que fuerza una conexión TCP.|tcp:APPHOST\SQLEXPRESS|  
|Conexión a una instancia predeterminada mediante la especificación de un nombre de canalización con nombre.|\\\APPHOST\pipe\unit\app|  
|Conexión a una instancia con nombre mediante la especificación de un nombre de canalización con nombre.|\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query|  
|Conexión a una instancia predeterminada por nombre, lo que fuerza una conexión de canalizaciones con nombre.|np:APPHOST|  
|Conexión a una instancia con nombre por nombre, lo que fuerza una conexión de canalizaciones con nombre.|np:APPHOST\SQLEXPRESS|  
  
## <a name="verifying-your-connection-protocol"></a>Comprobar el protocolo de conexión  
 Cuando se conecta a [!INCLUDE[ssDE](../../includes/ssde-md.md)], la siguiente consulta devolverá el protocolo usado para la conexión actual, junto con el método de autenticación (NTLM o Kerberos), e indicará si la conexión está cifrada.  
  
```tsql  
SELECT net_transport, auth_scheme, encrypt_option   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 [Iniciar una sesión en una instancia de SQL Server &#40;símbolo del sistema&#41;](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)  
  
 Los recursos siguientes pueden ayudarle a solucionar problemas de conexión.  
  
-   [Cómo solucionar problemas de conexión al motor de base de datos de SQL Server](http://social.technet.microsoft.com/wiki/contents/articles/how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
-   [Pasos para solucionar problemas de conectividad de SQL](http://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
## <a name="related-content"></a>Contenido relacionado  
 [Elegir un modo de autenticación](../../relational-databases/security/choose-an-authentication-mode.md)  
  
 [Usar la utilidad sqlcmd](../../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
 [Crear un inicio de sesión](../../t-sql/lesson-2-1-creating-a-login.md)  
  
  
