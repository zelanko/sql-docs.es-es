---
title: "Configuración de red del dispositivo (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8e2b9abe-963d-479b-a4a7-1739fcb3e249
caps.latest.revision: "27"
ms.openlocfilehash: e24ed8e992591d08628ffeb14c30a47d7fa5b54a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="appliance-network-configuration"></a>Configuración de red del dispositivo
El dispositivo PDW de SQL Server está creado y configurado con un conjunto de corrección de direcciones IP a lo largo de todos los servidores y dispositivos aplicables de fábrica del IHV. Con la entrega del dispositivo, la dirección de IP externas (Ethernet) debe configurarse para que coincida con los requisitos de centro de datos del cliente específico.  
  
> [!NOTE]  
> PDW V1 requerido 8 externo IP (*orientada hacia el cliente*) nodos de bastidor de direcciones para proporcionar conectividad externa a cada uno del control. PDW 2012 (V2) había mejorado de las comunicaciones de red mediante la exposición de todos los componentes del dispositivo de forma externa a través de direcciones IP. Este enfoque proporciona un diseño más eficaz que reduce los costos y aumenta la flexibilidad y mejora el movimiento de datos, la carga de datos y la integración de Hadoop. El número de direcciones IP necesarias depende del número de nodos en el dispositivo y la presencia de características como HDInsight. Para dar cabida a este bloque mayor de direcciones IP, el cliente deberá configurar una subred independiente para PDW. En esta subred, habrá suficiente espacio de direcciones IP (hasta 250 direcciones) para dar cabida a los componentes de hasta 5 bastidores PDW.  
  
El **configuración de red** página le permite ver la configuración de red con orientación externa para los nodos en el dispositivo de sistema de la plataforma de análisis. Esta página es de solo lectura.  
  
![Red de dispositivo de DWConfig](./media/appliance-network-configuration/SQL_Server_PDW_DWConfig_ApplTopNetwork.png "SQL_Server_PDW_DWConfig_ApplTopNetwork")  
  
## <a name="to-update-the-network-configuration-on-your-appliance"></a>Para actualizar la configuración de red en el dispositivo  
Cambiar las direcciones IP del dominio de tejido, dominio de la carga de trabajo y dominios de HDInsight editando el **AplianceInfo.xml** archivo y, a continuación, ejecutar el programa de instalación. Se trata de una operación sin conexión. El PDW y HDInsight (si está presente) regiones se interrumpirá automáticamente durante el cambio de dirección IP.  
  
> [!NOTE]  
> Nombres de dominio se proporcionan durante la instalación y se especifican como hasta 6 caracteres alfanuméricos, empiece por una letra. Un sistema de nomenclatura frecuente crea un dominio de tejido a partir de F, un dominio de la carga de trabajo PDW a partir de P y un dominio de HDInsight a partir de H. Este formato se supone en todos los temas de archivo de ayuda, pero no es necesario. <!-- MISSING LINKS For more information about the domain structure, see [PDW Domain Security &#40;SQL Server PDW&#41;](../sqlpdw/pdw-domain-security-sql-server-pdw.md) and [Understanding the Security Model of the HDInsight Region &#40;Analytics Platform System&#41;](../hdinsight/understanding-the-security-model-of-the-hdinsight-region.md)  -->  
  
#### <a name="to-change-the-ip-addresses-of-the-analytics-platform-system"></a>Para cambiar las direcciones IP de Analytics Platform System  
  
1.  Mediante el **escritorio remoto** aplicación, conectarse a **HST01** con la cuenta de administrador de dominio de carga de trabajo.  
  
2.  En el nodo HST01, abra el archivo de información de dispositivo de **c:\pdwinst\media\AplianceInfo.xml**.  
  
    > [!NOTE]  
    > Si el archivo no está presente, puede deben crearse un nuevo archivo.  
  
3.  Actualice los valores de Ethernet IP según sea necesario y guarde el archivo.  
  
4.  En una ventana del símbolo del sistema, ejecute el siguiente comando de instalación para actualizar las direcciones IP para la región PDW, con los nombres de dominio de P/F/H y las contraseñas de administrador.  
  
    ```  
    c:\pdwinst\media\setup.exe /action="ConfigureEthernet" /DomainAdminPassword="<password>" /ApplianceInfoFile="C:\PDWINST\media\ApplianceInfo.xml"  
    ```  
  
## <a name="manufacturer-references"></a>Referencias de fabricante  
Para obtener información adicional acerca de los dispositivos de Dell, vea:  
  
-   Instrucciones Switch PowerConnect [Guía de referencia de Dell PowerConnect 6200 serie sistema CLI](http://downloads.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_powerconnect/powerconnect-6224f_Reference%20Guide_en-us.pdf)  
  
-   iDRAC/BMC [manual del usuario integrada Dell remoto acceso controlador 7 (iDRAC7) versión 1.30.30](http://downloads.dell.com/Manuals/all-products/esuprt_electronics/esuprt_software/esuprt_remote_ent_sys_mgmt/integrated-dell-remote-access-cntrllr-7-v1.30.30_User%27s%20Guide_en-us.pdf?c=us&l=en&cs=555&s=biz)  
  
-   De la PDU **Rack PDU limitados de Dell**`ftp://ftp.dell.com/Manuals/all-products/esuprt_ser_stor_net/esuprt_rack_infrastructure/dell-metered-pdu-led_User's%20Guide_en-us.pdf`  
  
## <a name="see-also"></a>Vea también  
[Inicie el Administrador de configuración &#40; Sistema de la plataforma de análisis &#41;](launch-the-configuration-manager.md)  
  
