---
title: Configuración de un grupo de disponibilidad de varias subredes y FCI (Linux)
description: Obtenga información sobre cómo configurar grupos de disponibilidad AlwaysOn e instancias de clúster de conmutación por error (FCI) de varias subredes para SQL Server en Linux.
ms.custom: seo-lt-2019
author: liweiSecurity
ms.author: liweiyin
ms.reviewer: VanMSFT
ms.date: 07/28/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 5abe1d99f753e0f41ca74a0864079293800dc1df
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362998"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Configuración de grupos de disponibilidad e instancias de clúster de conmutación por error AlwaysOn de varias subredes

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Cuando un grupo de disponibilidad (AG) o una instancia de clúster de conmutación por error (FCI) AlwaysOn abarca más de un sitio, cada sitio suele tener sus propias redes. Esto normalmente significa que cada sitio tiene sus propias direcciones IP. Por ejemplo, las direcciones del sitio A empiezan por 192.168.1.*x*, mientras que las del sitio B comienzan por 192.168.2.*x*, donde *x* es la parte de la dirección IP que es única para el servidor. Si no hay aplicado ningún tipo de enrutamiento en el nivel de red, estos servidores no pueden comunicarse entre sí. Hay dos formas de controlar este escenario: configurar una red entre las dos subredes diferentes, lo que se conoce como VLAN, o configurar el enrutamiento entre las subredes.

## <a name="vlan-based-solution"></a>Solución basada en VLAN
 
**Requisito previo**: En el caso de una solución basada en VLAN, cada servidor que participa en un grupo de disponibilidad o una instancia de conmutación por error necesita dos tarjetas de red (NIC) para una disponibilidad adecuada (una NIC de puerto doble sería un solo punto de error en un servidor físico), a fin de que se le puedan asignar direcciones IP en su subred nativa, así como una en la VLAN. Esto se suma a cualquier otra necesidad de red, como iSCSI, que también necesita su propia red.

La creación de la dirección IP para el grupo de disponibilidad o la instancia de clúster de conmutación por error se realiza en la VLAN. En el ejemplo siguiente, la VLAN tiene una subred de 192.168.3.*x*, por lo que la dirección IP creada para el grupo de disponibilidad o la instancia de clúster de conmutación por error es 192.168.3.104. No es necesario configurar nada más, ya que hay una dirección IP única asignada al grupo de disponibilidad o la instancia de conmutación por error.

![Configuración de varias subredes 01](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Configuración con Pacemaker

En el entorno Windows, un clúster de conmutación por error de Windows Server (WSFC) admite de forma nativa varias subredes y administra varias direcciones IP a través de una dependencia OR en la dirección IP. En Linux, no hay ninguna dependencia OR, pero hay una manera de lograr una subred múltiple adecuada de forma nativa con Pacemaker, como se muestra a continuación. No puede hacer esto simplemente con la línea de comandos normal de Pacemaker para modificar un recurso. Debe modificar la base de información del clúster (CIB). CIB es un archivo XML con la configuración de Pacemaker.

![Configuración de varias subredes 02](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Actualización del CIB

1. Exporte el CIB.

    **Red Hat Enterprise Linux (RHEL) y Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    Donde *filename* es el nombre que quiere asignar al CIB.

2. Edite el archivo generado. Busque la sección `<resources>`. Se ven los distintos recursos creados para el grupo de disponibilidad o la instancia de clúster de conmutación por error. Busque el asociado a la dirección IP. Agregue una sección `<instance attributes>` con la información de la segunda dirección IP, ya sea por encima o por debajo de la existente, pero antes de `<operations>`. Es similar a la siguiente sintaxis:

    ```xml
    <instance attributes id="<NameForAttribute>">
        <nvpair id="<NameForIP>" name="ip" value="<IPAddress>"/>
    </instance attributes>
    ```
    
    donde *NameForAttribute* es el nombre único de este atributo, *NameForIP* es el nombre asociado a la dirección IP e *IPAddress* es la dirección IP de la segunda subred.
    
    A continuación se muestra un ejemplo.
    
    ```xml
    <instance attributes id="virtualip-instance_attributes">
        <nvpair id="virtualip-instance_attributes-ip" name="ip" value="192.168.1.102"/>
    </instance attributes>
    ```
    
    De forma predeterminada, solo hay un objeto <instance/> en el archivo XML CIB exportado. Supongamos que hay dos subredes, por lo que debe tener dos entradas <instance/>.
    Este es un ejemplo de entradas para dos subredes.
    
    ```xml
    <instance attributes id="virtualip-instance_attributes1">
        <rule id="Subnet1-IP" score="INFINITY" boolean-op="or">
            <expression id="Subnet1-Node1" attribute="#uname" operation="eq" value="Node1" />
            <expression id="Subnet1-Node2" attribute="#uname" operation="eq" value="Node2" />
        </rule>
        <nvpair id="IP-In-Subnet1" name="ip" value="192.168.1.102"/>
    </instance attributes>
    <instance attributes id="virtualip-instance_attributes2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node1" attribute="#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet2" name="ip" value="192.168.2.102"/>
    </instance attributes>
    ```
   
   Se usa 'boolean-op="or"' cuando la subred tiene más de un servidor.


3. Importe el CIB modificado y vuelva a configurar Pacemaker.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    donde *filename* es el nombre del archivo CIB con la información de dirección IP modificada.

### <a name="check-and-verify-failover"></a>Comprobación de la conmutación por error

1. Después de que el CIB se haya aplicado correctamente con la configuración actualizada, haga ping al nombre DNS asociado al recurso de dirección IP en Pacemaker. Debe reflejar la dirección IP asociada a la subred que hospeda actualmente el grupo de disponibilidad o la instancia de clúster de conmutación por error.

2. Conmute el grupo de disponibilidad o la instancia de clúster de conmutación por error en la otra subred.

3. Una vez que el grupo de disponibilidad o la instancia de clúster de conmutación por error estén totalmente en línea, haga ping al nombre DNS asociado a la dirección IP. Debe reflejar la dirección IP de la segunda subred.

4. Si quiere, conmute el grupo de disponibilidad o la instancia de clúster de conmutación por error en la subred original.

Esta es una publicación de CSS en la que se muestra cómo configurar CIB para tres subredes. Para obtener más información, consulte [Configuración del grupo de disponibilidad AlwaysOn de varias subredes mediante la modificación de CIB](https://techcommunity.microsoft.com/t5/sql-server-support/configure-multiple-subnet-alwayson-availability-groups-by/ba-p/1544838).
