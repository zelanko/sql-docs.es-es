---
title: Configuración de la red del dispositivo
description: El dispositivo Analytics Platform System (APS) se crea y se configura con un conjunto de direcciones IP en todos los servidores y los dispositivos aplicables de la fábrica del IHV. Tras la entrega del dispositivo, la dirección IP externa (Ethernet) debe volver a configurarse para que coincida con los requisitos del centro de datos del cliente específico.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: af892cbb43b42953732bda59d371e3e22855413b
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401411"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Configuración de red del dispositivo de Analytics Platform System
El dispositivo Analytics Platform System (APS) se crea y se configura con un conjunto de direcciones IP en todos los servidores y los dispositivos aplicables de la fábrica del IHV. Tras la entrega del dispositivo, la dirección IP externa (Ethernet) debe volver a configurarse para que coincida con los requisitos del centro de datos del cliente específico.  
  
> [!NOTE]  
> PDW V1 requirió 8 direcciones IP externas (de*cara al cliente*) para proporcionar conectividad externa a cada uno de los nodos del bastidor de control. Las comunicaciones de red mejoradas de PDW 2012 (V2) exponen todos los componentes del dispositivo externamente a través de direcciones IP. Este enfoque proporciona un diseño más sólido que reduce los costos y aumenta la flexibilidad, y mejora el movimiento de datos, la carga de datos y la integración de Hadoop. El número de direcciones IP necesario depende del número de nodos del dispositivo. Para dar cabida a este bloque mayor de direcciones IP, el cliente debe configurar una subred independiente para PDW. Dentro de esta subred, habrá suficiente espacio de direcciones IP (hasta 250 direcciones) para dar cabida a los componentes de hasta 5 bastidores de PDW.  
  
La página **configuración de red** le permite ver la configuración de red orientada externamente a los nodos del dispositivo de análisis de plataforma de Analytics. Esta página es de solo lectura.  
  
![Red HDI del dispositivo DWConfig](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>Para actualizar la configuración de red en el dispositivo  
Cambie las direcciones IP del dominio del tejido y el dominio de la carga de trabajo editando el archivo **AplianceInfo. XML** y ejecutando el programa de instalación. Se trata de una operación sin conexión. Las regiones de PDW se detendrán automáticamente durante el cambio de dirección IP.  
  
> [!NOTE]  
> Los nombres de dominio se proporcionan durante la instalación y se especifican hasta 6 caracteres alfanuméricos, empezando por una letra. Un sistema de nomenclatura frecuente crea un dominio de tejido que empieza con F, un dominio de carga de trabajo de PDW que empieza por P. Este formato se presupone en los temas del archivo de ayuda, pero no es necesario. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Para cambiar las direcciones IP del sistema de plataforma de análisis  
  
1.  Mediante la aplicación de **escritorio remoto** , conéctese a **HST01** con la cuenta de administrador de dominio de carga de trabajo.  
  
2.  En el nodo HST01, abra el archivo de información del dispositivo en **c:\pdwinst\media\AplianceInfo.XML**.  
  
    > [!NOTE]  
    > Si el archivo no está presente, es posible que sea necesario crear un nuevo archivo.  
  
3.  Actualice los valores IP de Ethernet según sea necesario y guarde el archivo.  
  
4.  En una ventana del símbolo del sistema, ejecute el siguiente comando de instalación para actualizar las direcciones IP de la región de PDW mediante los nombres de dominio P/F/H y las contraseñas de administrador.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>Referencias del fabricante  
Para obtener información adicional acerca de los dispositivos Dell, consulte:  
  
-   Instrucciones del conmutador PowerConnect guía de referencia de la [CLI del sistema de Dell powerconnect 6200](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   [Guía de usuario de iDRAC/BMC integrada de Dell Remote Access Controller 7 (iDRAC7) 1.30.30](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   PDU de **bastidor de uso medido de Dell** para PDU`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>Véase también  
[Inicie el sistema de Configuration Manager &#40;Analytics Platform&#41;](launch-the-configuration-manager.md)  
  
