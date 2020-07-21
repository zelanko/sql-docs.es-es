---
title: Configuración de un grupo de disponibilidad de varias subredes y FCI (Linux)
description: Obtenga información sobre cómo configurar grupos de disponibilidad AlwaysOn e instancias de clúster de conmutación por error (FCI) de varias subredes para SQL Server en Linux.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 12/01/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 3a18e668d1a62a74396530e37243d75a5a86aee2
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196973"
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
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    donde *NameForAttribute* es el nombre único de este atributo, *Score* es el número asignado al atributo, que debe ser mayor que el de la subred principal, *RuleName* es el nombre de la regla, *ExpressionName* es el nombre de la expresión, *NodeNameInSubnet2* es el nombre del nodo de la otra subred, *NameForSecondIP* es el nombre asociado a la segunda dirección IP, *IPAddress* es la dirección IP de la segunda subred, *NameForSecondIPNetmask* es el nombre asociado a la máscara de red y *Netmask* es la máscara de red de la segunda subred.
    
    A continuación se muestra un ejemplo.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

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
