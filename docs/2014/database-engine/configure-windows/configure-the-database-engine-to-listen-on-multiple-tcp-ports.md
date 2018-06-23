---
title: Configurar el motor de base de datos para escuchar en varios puertos TCP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ports [SQL Server], multiple
- TDS
- listen on multiple ports
- endpoints [SQL Server], TDS
- adding ports
- tabular data stream
- multiple ports
ms.assetid: 8e955033-06ef-403f-b813-3d8241b62f1f
caps.latest.revision: 25
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 766c72f478be2cce2688312ed3accd43e67998b5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202348"
---
# <a name="configure-the-database-engine-to-listen-on-multiple-tcp-ports"></a>Configurar el motor de base de datos para escuchar en varios puertos TCP
  En este tema se describe cómo configurar el [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que escuche en varios puertos TCP en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. Si se ha habilitado TCP/IP para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el [!INCLUDE[ssDE](../../includes/ssde-md.md)] escuchará las conexiones entrantes en un punto de conexión compuesto por una dirección IP y un número de puerto TCP. Los procedimientos siguientes crean un extremo de flujo TDS para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuche en otro puerto TCP.  
  
 A continuación se detallan algunos posibles motivos que pueden llevar a crear un segundo extremo de TDS:  
  
-   Incrementar la seguridad configurando el firewall de modo que se restrinja el acceso al extremo predeterminado a equipos cliente locales de una subred específica. Mantener el acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de Internet para el equipo de soporte creando un nuevo extremo que quede expuesto a Internet a través del firewall y restringiendo los derechos de conexión a este extremo al equipo de soporte del servidor.  
  
-   Establecer afinidades entre conexiones y procesadores específicos al utilizar acceso no uniforme a memoria (NUMA).  
  
 Para configurar un extremo de TDS hay que realizar los siguientes pasos, que se pueden efectuar en cualquier orden:  
  
-   Cree el extremo de TDS para el puerto TCP y restaure el acceso al extremo predeterminado si procede.  
  
-   Conceda acceso al extremo a las entidades de seguridad de servidor que desee.  
  
-   Especifique el número de puerto TCP para la dirección IP seleccionada.  
  
 Para obtener más información sobre la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan al motor de base de datos, Analysis Services, Reporting Services e Integration Services, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
##  <a name="SSMSProcedure"></a>  
  
#### <a name="to-create-a-tds-endpoint"></a>Para crear un extremo de TDS  
  
-   Ejecute la siguiente instrucción para crear un extremo denominado **CustomConnection** para el puerto 1500, para todas las direcciones TCP disponibles en el servidor.  
  
    ```  
    USE master;  
    GO  
    CREATE ENDPOINT [CustomConnection]  
    STATE = STARTED  
    AS TCP  
       (LISTENER_PORT = 1500, LISTENER_IP =ALL)  
    FOR TSQL() ;  
    GO  
    ```  
  
 Cuando se crea un nuevo extremo de [!INCLUDE[tsql](../../includes/tsql-md.md)] , los permisos de conexión correspondientes a **public** se revocan para el extremo de TDS predeterminado. Si el acceso al grupo **public** es necesario para el extremo predeterminado, aplique de nuevo este permiso mediante la instrucción `GRANT CONNECT ON ENDPOINT::[TSQL Default TCP] to [public];` .  
  
#### <a name="to-grant-access-to-the-endpoint"></a>Para conceder acceso al extremo  
  
-   Ejecute la siguiente instrucción para conceder acceso al extremo **CustomConnection** al grupo de soporte de SQL en el dominio corporativo.  
  
    ```  
    GRANT CONNECT ON ENDPOINT::[CustomConnection] to [corp\SQLSupport] ;  
    GO  
    ```  
  
#### <a name="to-configure-the-sql-server-database-engine-to-listen-on-an-additional-tcp-port"></a>Para configurar el motor de la base de datos de SQL Server para escuchar en otro puerto TCP  
  
1.  En Administrador de configuración de SQL Server, expanda **Configuración de red de SQL Server** y, después, haga clic en **Protocolos de***<nombre_de_instancia>*.  
  
2.  Expanda **Protocolos de***<nombre_de_instancia>* y, después, haga clic en **TCP/IP**.  
  
3.  En el panel derecho, haga clic con el botón derecho en cada dirección IP deshabilitada que quiera habilitar y, después, haga clic en **Habilitar**.  
  
4.  Haga clic con el botón derecho en **IPAll**y, después, haga clic en **Propiedades**.  
  
5.  En el cuadro **Puerto TCP** , escriba los puertos en los que desee que escuche el [!INCLUDE[ssDE](../../includes/ssde-md.md)] , separados por comas. En nuestro ejemplo, si aparece el puerto predeterminado 1433, escriba `,1500` por lo que el cuadro se lea `1433,1500`y, a continuación, haga clic en **Aceptar**.  
  
    > [!NOTE]  
    >  Si no va a habilitar el puerto en todas las direcciones IP, configure el puerto adicional en el cuadro de propiedades solo para la dirección deseada. Después, en el panel de la consola, haga clic con el botón derecho en **TCP/IP**, haga clic en **Propiedades**y, en el cuadro **Escuchar todo** , seleccione **No**.  
  
6.  En el panel izquierdo, haga clic en **Servicios de SQL Server**.  
  
7.  En el panel derecho, haga clic con el botón derecho en **SQL Server***<nombre_de_instancia>* y, después, haga clic en **Reiniciar**.  
  
     Cuando se reinicie el [!INCLUDE[ssDE](../../includes/ssde-md.md)], el registro de errores mostrará los puertos en los que escucha [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
#### <a name="to-connect-to-the-new-endpoint"></a>Para conectarse al nuevo extremo  
  
-   Ejecute la siguiente instrucción para conectarse al punto de conexión **CustomConnection** de la instancia predeterminada de SQL Server en el servidor llamado ACCT, usando una conexión de confianza y suponiendo que el usuario es miembro del grupo [corp\SQLSupport].  
  
    ```  
    sqlcmd -SACCT,1500  
    ```  
  
## <a name="see-also"></a>Vea también  
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [DROP ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-endpoint-transact-sql)   
 [GRANT &#40;permisos de punto de conexión de Transact-SQL&#41;](/sql/t-sql/statements/grant-endpoint-permissions-transact-sql)   
 [Asignación de puertos TCP/IP a nodos NUMA &#40;SQL Server&#41;](map-tcp-ip-ports-to-numa-nodes-sql-server.md)  
  
  
