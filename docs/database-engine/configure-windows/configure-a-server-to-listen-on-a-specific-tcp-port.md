---
title: Configurar un servidor para que escuche en un puerto TCP específico | Microsoft Docs
description: Aprenda a usar el Administrador de configuración de SQL Server para configurar el Motor de base de datos para que escuche en un puerto fijo específico que no sea el predeterminado, 1433.
ms.custom: ''
ms.date: 04/25/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- fixed port
- static ports
- ports [SQL Server], assigning numbers
- assigning port numbers
- dynamic ports [SQL Server]
- TCP/IP [SQL Server], port numbers
ms.assetid: 2276a5ed-ae3f-4855-96d8-f5bf01890640
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 15d1d1ab04adb47772706f8b1495b8ddef8b4fa3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789840"
---
# <a name="configure-a-server-to-listen-on-a-specific-tcp-port"></a>Configurar un servidor para que escuche en un puerto TCP específico
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  En este tema se describe cómo configurar una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para escuchar en un puerto fijo específico mediante el Administrador de configuración de SQL Server. Si está habilitada, la instancia predeterminada de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escucha en el puerto TCP 1433. Las instancias con nombre de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssEW](../../includes/ssew-md.md)] están configuradas para [puertos dinámicos](../../tools/configuration-manager/tcp-ip-properties-ip-addresses-tab.md). Esto significa que seleccionan un puerto disponible cuando se inicia el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando se conecte a una instancia con nombre a través de un firewall, configure el [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que escuche en un puerto específico, de modo que el puerto adecuado pueda abrirse en el firewall.  

Dado que el puerto 1433 es el estándar conocido de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], en algunas organizaciones se indica que conviene cambiar el número de puerto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para mejorar la seguridad. Esto puede resultar útil en algunos entornos. A pesar de esto, las arquitecturas de TCP/IP permiten que un [examinador de puertos](https://wikipedia.org/wiki/Port_scanner) consulte cuáles son los puertos abiertos, de modo que cambiar el número de puerto no se considera una medida de seguridad eficaz.

 Para obtener más información sobre la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan al motor de base de datos, Analysis Services, Reporting Services e Integration Services, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
> [!TIP]  
>  Al seleccionar un número de puerto, consulte [https://www.iana.org/assignments/port-numbers](https://www.iana.org/assignments/port-numbers) para obtener una lista de los números de puerto asignados a determinadas aplicaciones. Seleccione un número de puerto sin asignar. Para obtener más información, vea [El rango de puertos dinámicos predeterminado para TCP/IP ha cambiado en Windows Vista y Windows Server 2008](https://support.microsoft.com/kb/929851).  
  
> [!WARNING]  
>  El Motor de base de datos empieza a escuchar en un puerto nuevo cuando se reinicia. Sin embargo, el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser supervisa el Registro e informa del nuevo número de puerto en cuanto cambia la configuración, incluso aunque el Motor de base de datos no lo use. Reinicie el Motor de base de datos para asegurar la coherencia y evitar errores de conexión.  
  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-assign-a-tcpip-port-number-to-the-sql-server-database-engine"></a>Para asignar un número de puerto TCP/IP al Motor de base de datos de SQL Server  
  
1.  En el panel de la consola del Administrador de configuración de SQL Server, expanda **Configuración de red de SQL Server**, **Protocolos de \<instance name>** y, después, haga doble clic en **TCP/IP**.  
  
    > [!NOTE]  
    >  Si tiene problemas para abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md).  
  
2.  En el cuadro de diálogo **Propiedades de TCP/IP** , en la pestaña **Direcciones IP** , aparecen varias direcciones IP con el formato **IP1**, **IP2**, hasta **IPAll**. Una de estas direcciones IP, 127.0.0.1, se utiliza para el adaptador de bucle invertido. Aparecen direcciones IP adicionales para cada dirección IP del equipo. (Probablemente verá direcciones IP de la versión 4 y la versión 6). Haga clic con el botón derecho en cada dirección y luego haga clic en **Propiedades** para identificar la dirección IP que quiera configurar.  
  
3.  Si el cuadro de diálogo **Puertos dinámicos TCP** contiene **0**, que indica que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] escucha en los puertos dinámicos, elimine el 0.  
  
     ![TCP_ports](../../database-engine/configure-windows/media/tcp-ports.png "TCP_ports")  
  
4.  En el cuadro **Propiedades** de **IP_n_**, en **Puerto TCP**, escriba el número de puerto en el que quiere que esta dirección IP escuche y haga clic en **Aceptar**. Para especificar varios puertos, sepárelos con una coma.

    > [!NOTE] 
    > Si la opción **Escuchar todo** de la pestaña **Protocolo** está establecida en "Sí", solo se usarán los valores de **Puerto TCP** y **Puerto dinámico TCP** de la sección **IPAll** y se ignorarán las secciones individuales **IP**_n_ en su totalidad. Si la opción **Escuchar todo** está establecida en "No", se ignorarán los ajustes de **Puerto TCP** y **Puerto dinámico TCP** de la sección **IPAll** y se usarán los valores de **Puerto TCP**, **Puerto dinámico TCP** y **Habilitado** de las secciones individuales **IP**_n_ en su lugar.
    > Cada sección **IP**_n_ tiene un ajuste **Habilitado** con un valor predeterminado de "No", lo que hace que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ignore esta dirección IP, incluso si tiene definido un puerto.  
  
5.  En el panel de la consola, haga clic en **Servicios de SQL Server**.  
  
6.  En el panel de detalles, haga clic con el botón derecho en **SQL Server (** \<instance name> **)** y, después, haga clic en **Reiniciar** para detener y reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="connecting"></a>Connecting  
Después de haber configurado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que escuche en un puerto específico, dispone de tres métodos para conectarse a un puerto específico con una aplicación cliente:  
  
-   Ejecute el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor para conectarse a la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] por nombre.  
-   Cree un alias en el cliente; para ello, especifique el número de puerto.  
-   Programar el cliente para conectarse mediante una cadena de conexión personalizada.  
  
## <a name="see-also"></a>Consulte también  
 [Crear o eliminar un alias de servidor para que lo utilice un cliente &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [Servicio SQL Server Browser](../../tools/configuration-manager/sql-server-browser-service.md)  
  
  
