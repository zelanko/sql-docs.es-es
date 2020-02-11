---
title: Configurar un servidor para que escuche en un puerto TCP específico (Administrador de configuración de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e85b1a85ab9415c76fdaeee5453c992994a286ba
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62813591"
---
# <a name="configure-a-server-to-listen-on-a-specific-tcp-port-sql-server-configuration-manager"></a>Configurar un servidor para que escuche en un puerto TCP específico (Administrador de configuración de SQL Server)
  En este tema se describe cómo configurar una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para escuchar en un puerto fijo específico mediante el Administrador de configuración de SQL Server. Si está habilitada, la instancia predeterminada de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escucha en el puerto TCP 1433. Las instancias con nombre de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssEW](../../includes/ssew-md.md)] están configuradas para puertos dinámicos. Esto significa que seleccionan un puerto disponible cuando se inicia el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando se conecte a una instancia con nombre a través de un firewall, configure el [!INCLUDE[ssDE](../../includes/ssde-md.md)] para que escuche en un puerto específico, de modo que el puerto adecuado pueda abrirse en el firewall.  
  
 Para obtener más información sobre la configuración predeterminada de Firewall de Windows y una descripción de los puertos TCP que afectan al motor de base de datos, Analysis Services, Reporting Services e Integration Services, vea [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
> [!TIP]  
>  Al seleccionar un número de puerto, [http://www.iana.org/assignments/port-numbers](http://www.iana.org/assignments/port-numbers) consulte para obtener una lista de los números de Puerto asignados a determinadas aplicaciones. Seleccione un número de puerto sin asignar. Para obtener más información, vea [El rango de puertos dinámicos predeterminado para TCP/IP ha cambiado en Windows Vista y Windows Server 2008](https://support.microsoft.com/kb/929851).  
  
> [!WARNING]  
>  El Motor de base de datos empieza a escuchar en un puerto nuevo cuando se reinicia. Sin embargo, el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser supervisa el Registro e informa del nuevo número de puerto en cuanto cambia la configuración, incluso aunque el Motor de base de datos no lo use. Reinicie el Motor de base de datos para asegurar la coherencia y evitar errores de conexión.  
  
 **En este tema**  
  
-   **Para configurar un servidor para que escuche en un puerto TCP específico, utilizando:**  
  
     [Administrador de configuración de SQL Server](#SSMSProcedure)  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-assign-a-tcpip-port-number-to-the-sql-server-database-engine"></a>Para asignar un número de puerto TCP/IP al Motor de base de datos de SQL Server  
  
1.  En Administrador de configuración de SQL Server, en el panel de la consola, expanda **SQL Server configuración de red**, expanda **protocolos \<para nombre de instancia>** y, a continuación, haga doble clic en **TCP/IP**.  
  
2.  En el cuadro de diálogo **Propiedades de TCP/IP**, en la pestaña **Direcciones IP**, aparecen varias direcciones IP con el formato **IP1**, **IP2**, hasta **IPAll**. Una de estas direcciones IP, 127.0.0.1, se utiliza para el adaptador de bucle invertido. Aparecen direcciones IP adicionales para cada dirección IP del equipo. Haga clic con el botón derecho en cada dirección y luego haga clic en **Propiedades** para identificar la dirección IP que quiera configurar.  
  
3.  Si el cuadro de diálogo **Puertos dinámicos TCP** contiene **0**, que indica que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] escucha en los puertos dinámicos, elimine el 0.  
  
4.  En el cuadro de área **propiedades** de **IP**_n_ , en el cuadro **puerto TCP** , escriba el número de puerto en el que desea que escuche esta dirección IP y, a continuación, haga clic en **Aceptar**.  
  
5.  En el panel de la consola, haga clic en **Servicios de SQL Server**.  
  
6.  En el panel de detalles, haga clic con el botón secundario en **SQL Server (**\<nombre de instancia>**)** y, a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]continuación, haga clic en **reiniciar**para detener y reiniciar.  
  
 Después de haber configurado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que escuche en un puerto específico, dispone de tres métodos para conectarse a un puerto específico con una aplicación cliente:  
  
-   Ejecute el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el servidor para conectarse a la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] por nombre.  
  
-   Cree un alias en el cliente; para ello, especifique el número de puerto.  
  
-   Programar el cliente para conectarse mediante una cadena de conexión personalizada.  
  
## <a name="see-also"></a>Consulte también  
 [Crear o eliminar un alias de servidor para que lo use un cliente &#40;Administrador de configuración de SQL Server&#41;](create-or-delete-a-server-alias-for-use-by-a-client.md)  
  
  
