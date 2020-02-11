---
title: Usar un reenviador DNS
description: Usar un reenviador DNS para resolver nombres DNS que no sean de aplicación en Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3d1d0d9428138da615fad7ff5745c758d9fcd3b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74399432"
---
# <a name="use-a-dns-forwarder-to-resolve-non-appliance-dns-names-in-analytics-platform-system"></a>Usar un reenviador DNS para resolver nombres DNS que no sean de aplicación en Analytics Platform System
Se puede configurar un reenviador DNS en el Active Directory Domain Services nodos (**_dominio de aplicación\__-AD01** y ** _dominio de aplicación\__-AD02**) del dispositivo de sistema de plataforma de análisis para permitir que los scripts y las aplicaciones de software tengan acceso a los servidores externos.  
  
## <a name="ResolveDNS"></a>Uso de un reenviador DNS  
El dispositivo Analytics Platform System se configura para evitar la resolución de nombres DNS de servidores que no están en el dispositivo. Algunos procesos, como Windows Software Update Services (WSUS), tendrán que acceder a los servidores fuera del dispositivo. Para admitir este escenario de uso, el DNS del sistema de plataforma de análisis puede configurarse para admitir un reenviador de nombres externo que permita que los hosts del sistema de plataforma de análisis y Virtual Machines (VM) usen servidores DNS externos para resolver nombres fuera del dispositivo. No se admite la configuración personalizada de sufijos DNS, lo que significa que debe usar nombres de dominio completos para resolver un nombre de servidor que no sea de dispositivo.  
  
**Para crear un reenviador DNS con la GUI de DNS**  
  
1.  Inicie sesión en el nodo ** _dominio\__-AD01 del dispositivo** .  
  
2.  Abra el administrador de DNS (**DNSMgmt. msc**).  
  
3.  Haga clic con el botón secundario en el nombre del servidor y, a continuación, haga clic en **propiedades**.  
  
4.  En la pestaña **Opciones avanzadas** , desactive la opción **deshabilitar recursividad (también deshabilita los reenviadores)** y, a continuación, haga clic en **aplicar**.  
  
5.  Haga clic en la pestaña **reenviadores** y, a continuación, haga clic en **Editar**.  
  
6.  Escriba la dirección IP del servidor DNS externo que va a proporcionar la resolución de nombres. Las máquinas virtuales y los servidores (hosts) del dispositivo se conectarán a los servidores externos mediante el uso de nombres de dominio completos.  
  
7.  Repita los pasos 1-6 en el nodo ** _dominio\__-AD02 del dispositivo**  
  
**Para crear un reenviador de DNS mediante Windows PowerShell**  
  
1.  Inicie sesión en el nodo ** _dominio\__-AD01 del dispositivo**.  
  
2.  Ejecute el siguiente script de Windows PowerShell desde el nodo ** _domain\__-AD01 del dispositivo** . Antes de ejecutar el script de Windows PowerShell, reemplace las direcciones IP por las direcciones IP de los servidores DNS que no son de la aplicación.  
  
    ```  
    $DNS=Get-WmiObject -class "MicrosoftDNS_Server"  -Namespace "root\microsoftdns"  
    $DNS.Forwarders = ("xxx.xxx.xxx.xxx", "xxx.xxx.xxx.xxx")  
    $DNS.put()  
    ```  
  
3.  Ejecute el mismo comando en el nodo ** _dominio\__-AD02 del dispositivo** .  
  
## <a name="configuring-dns-resolution-for-wsus"></a>Configuración de la resolución DNS para WSUS  
PDW de SQL Server 2012 proporciona funciones integradas de mantenimiento y revisión. PDW de SQL Server usa Microsoft Update y otras tecnologías de servicio de Microsoft. Para habilitar las actualizaciones, el dispositivo debe ser capaz de conectarse a un repositorio WSUS corporativo o al repositorio público de Microsoft WSUS.  
  
En el caso de los clientes que decidan configurar el dispositivo para buscar actualizaciones en el repositorio público de Microsoft WSUS, las instrucciones siguientes establecen los detalles de configuración adecuados en el dispositivo.  
  
> [!NOTE]  
> El administrador de red del cliente debe proporcionar la dirección IP de un servidor DNS corporativo que pueda resolver nombres en **Microsoft.com**.  
  
1.  Con el escritorio remoto, inicie sesión en la máquina<fabric domain>virtual de VMM (-VMM) con la cuenta de administrador de dominio de tejido.  
  
2.  Abra el panel de control, haga clic en **red e Internet**y, a continuación, haga clic en **centro de redes y recursos compartidos**.  
  
3.  En la lista conexión, haga clic en **VMSEthernet**y, a continuación, haga clic en **propiedades**.  
  
4.  Seleccione **Protocolo de Internet versión 4 (TCP/IPv4)** y luego haga clic en **Propiedades**.  
  
5.  En el cuadro **servidor DNS alternativo** , agregue la dirección IP proporcionada por el administrador de red del cliente.  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
