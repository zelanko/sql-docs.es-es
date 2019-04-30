---
title: 'Configuración de red del dispositivo: Analytics Platform System | Microsoft Docs'
description: El dispositivo de Analytics Platform System (APS) está creado y configurado con un conjunto de corrección de las direcciones IP a lo largo de todos los servidores y dispositivos aplicables de fábrica del IHV. Cuando se entrega el dispositivo, la dirección IP externa (Ethernet) debe reconfigurarse para satisfacer las necesidades de centro de datos del cliente específico.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: dc0fbd64ac1179cc77e5b8a3cf9f0e5fed73d7fd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63276113"
---
# <a name="appliance-network-configuration-for-analytics-platform-system"></a>Configuración de red del dispositivo para Analytics Platform System
El dispositivo de Analytics Platform System (APS) está creado y configurado con un conjunto de corrección de las direcciones IP a lo largo de todos los servidores y dispositivos aplicables de fábrica del IHV. Cuando se entrega el dispositivo, la dirección IP externa (Ethernet) debe reconfigurarse para satisfacer las necesidades de centro de datos del cliente específico.  
  
> [!NOTE]  
> PDW V1 necesario 8 externo IP (*orientado a clientes*) nodos en bastidor direcciones para proporcionar conectividad externa a cada uno del control. PDW 2012 (V2) ha mejorado las comunicaciones de red mediante la exposición de todos los componentes del dispositivo externamente a través de direcciones IP. Este enfoque proporciona un diseño más eficaz que reduce los costos y aumenta la flexibilidad y mejora la integración de Hadoop, la carga de datos y movimiento de datos. El número de direcciones IP requeridas depende del número de nodos en el dispositivo. Para dar cabida a este bloque mayor de direcciones IP, el cliente debe configurar una subred independiente para PDW. En esta subred, habrá suficiente espacio de direcciones IP (hasta 250 direcciones) para dar cabida a los componentes de hasta 5 bastidores PDW.  
  
El **configuración de red** página permite ver la configuración de red con orientación externa para los nodos en el dispositivo de Analytics Platform System. Esta página es de solo lectura.  
  
![Red de dispositivo de DWConfig](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>Para actualizar la configuración de red en el dispositivo  
Cambiar las direcciones IP de los dominios de fabric y carga de trabajo mediante la edición del **AplianceInfo.xml** archivo y, a continuación, ejecute el programa de instalación. Se trata de una operación sin conexión. Las regiones PDW se detendrá automáticamente durante el cambio de dirección IP.  
  
> [!NOTE]  
> Los nombres de dominio se proporcionan durante la instalación y se especifican como máximo de 6 caracteres alfanuméricos, empezando por una letra. Un sistema de nombres frecuente crea un dominio de fabric a partir de F, un dominio de carga de trabajo PDW a partir de P. Este formato se supone que a lo largo de los temas de ayuda, pero no es necesario. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Para cambiar las direcciones IP de la Analytics Platform System  
  
1.  Mediante el **escritorio remoto** aplicación, conéctese a **HST01** con la cuenta de administrador de dominio de carga de trabajo.  
  
2.  En el nodo HST01, abra el archivo de información de dispositivo en **c:\pdwinst\media\AplianceInfo.xml**.  
  
    > [!NOTE]  
    > Si el archivo no está presente, es posible que deben crearse un nuevo archivo.  
  
3.  Actualice los valores de Ethernet IP según sea necesario y guarde el archivo.  
  
4.  En una ventana del símbolo del sistema, ejecute el siguiente comando de instalación para actualizar las direcciones IP para la región PDW, con los nombres de dominio P, F/H y las contraseñas de administrador.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>Referencias de fabricante  
Para obtener más información acerca de los dispositivos de Dell, consulte:  
  
-   Instrucciones Switch PowerConnect [guía hacen referencia a Dell PowerConnect 6200 serie sistema CLI](https://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC [manual del usuario de versión 1.30.30 integrado Dell remoto acceso controlador 7 (iDRAC7)](https://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   De la PDU **Dell mide PDU bastidor**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>Vea también  
[Inicie el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
  
