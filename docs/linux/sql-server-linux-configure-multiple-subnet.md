---
title: Configurar varias subredes grupos de disponibilidad AlwaysOn y las instancias de clúster de conmutación por error en Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/1/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 0952390e21d174d4d10e99f53904de4d11be6230
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47637480"
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Configurar varias subredes grupos de disponibilidad AlwaysOn y las instancias de clúster de conmutación por error

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Cuando una instancia en clúster siempre en grupo de disponibilidad (AG) o la conmutación por error (FCI) abarca más de un sitio, cada sitio normalmente tiene su propia red. A menudo, esto significa que cada sitio tiene su propia dirección IP. Por ejemplo, direcciones de sitio del empiezan por 192.168.1. *x* e iniciar las direcciones del sitio B con 192.168.2. *x*, donde *x* es la parte de la dirección IP que es única para el servidor. Sin algún tipo de enrutamiento en su lugar en el nivel de red, estos servidores no podrán comunicarse entre sí. Hay dos formas de controlar este escenario: configurar una red que relaciona las dos subredes diferentes, conocidas como una VLAN, o configurar el enrutamiento entre subredes.

## <a name="vlan-based-solution"></a>Solución basada en VLAN
 
**Requisitos previos**: solución basada en para una VLAN, cada servidor que participe en un grupo de disponibilidad o FCI necesita dos tarjetas de red (NIC) para disponibilidad adecuada (un puerto dual de NIC sería un único punto de error en un servidor físico), por lo que se pueden asignar direcciones IP en su subred nativo, así como uno de la VLAN. Esto es además de otras necesidades de red, como iSCSI, que también necesita su propia red.

La creación de la dirección IP para el grupo de disponibilidad o FCI se realiza en la VLAN. En el ejemplo siguiente, la VLAN tiene una subred de 192.168.3. *x*, por lo que la dirección IP creada para el grupo de disponibilidad o FCI es 192.168.3.104. Nada adicional debe configurarse, ya que no hay una única dirección IP asignada al grupo de disponibilidad o FCI.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Configuración de Pacemaker

En el mundo de Windows, un clúster de conmutación por error de Windows Server (WSFC) de forma nativa es compatible con varias subredes y controla varias direcciones IP a través de una dependencia OR en la dirección IP. En Linux, no hay ninguna dependencia OR, pero hay una forma de lograr una correcta múltiples subredes de forma nativa con Pacemaker, como se muestra en la siguiente. No puede hacerlo simplemente con la línea de comandos normal de Pacemaker para modificar un recurso. Deberá modificar la información del clúster base (CIB). El CIB es un archivo XML con la configuración de Pacemaker.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Actualizar el CIB

1.  Exporte el CIB.

    **Red Hat Enterprise Linux (RHEL) y Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    Donde *filename* es el nombre que desea llamar el CIB.

2.  Edite el archivo que se generó. Busque el `<resources>` sección. Verá los distintos recursos que se crearon para el grupo de disponibilidad o FCI. Buscar el único asociado con la dirección IP. Agregar un `<instance attributes>` sección con la información de la segunda dirección IP por encima o debajo de la existente, pero antes `<operations>`. Es similar a la siguiente sintaxis:

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    donde *NameForAttribute* es el nombre único para este atributo, *puntuación* es el número asignado al atributo, que debe ser mayor que la subred principal, *RuleName*es el nombre de la regla, *ExpressionName* es el nombre de la expresión, *NodeNameInSubnet2* es el nombre del nodo en la otra subred *NameForSecondIP* es el nombre asociado con la segunda dirección IP, *IPAddress* es la dirección IP para la segunda subred, *NameForSecondIPNetmask* es el nombre asociado con la máscara de red, y *Máscara de red* es la máscara de red para la segunda subred.
    
    A continuación muestra un ejemplo.
    
    ```xml
    <instance attributes id="Node3-2nd-IP" score="2">
        <rule id="Subnet2-IP" score="INFINITY">
            <expression id="Subnet2-Node" attribute="\#uname" operation="eq" value="Node3" />
        </rule>
        <nvpair id="IP-In-Subnet-2" name="ip" value="192.168.2.102"/>
        <nvpair id="Netmask-For-IP2" name="cidr\_netmask" value="24" />
    </instance attributes>
    ```

3.  Importar el CIB modificada y vuelva a configurar a Pacemaker.

    **RHEL y Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    donde *filename* es el nombre del archivo CIB con la información de dirección IP modificada.

### <a name="check-and-verify-failover"></a>Compruebe y confirme la conmutación por error

1.  Una vez el CIB correctamente aplicada con la configuración actualizada, haga ping al nombre DNS asociado al recurso de dirección IP en Pacemaker. Debe reflejar la dirección IP asociada con la subred que hospeda el grupo de disponibilidad o FCI.
2.  Producirá un error en el grupo de disponibilidad o FCI para la otra subred.
3.  Después de que el grupo de disponibilidad o FCI está totalmente en línea, haga ping al nombre DNS asociado con la dirección IP. Debe reflejar la dirección IP en la segunda subred.
4.  Si lo desea, el grupo de disponibilidad o FCI conmutar por recuperación a la subred original.
