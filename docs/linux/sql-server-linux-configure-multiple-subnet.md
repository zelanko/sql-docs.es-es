---
title: Configurar instancias de clúster de conmutación por error y varias subredes grupos de disponibilidad AlwaysOn en Linux | Documentos de Microsoft
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/1/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 79695f234666111530e3f13cfbb9234eebfdd0c2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="configure-multiple-subnet-always-on-availability-groups-and-failover-cluster-instances"></a>Configurar instancias de clúster de conmutación por error y varias subredes grupos de disponibilidad AlwaysOn

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Cuando una instancia en clúster siempre en disponibilidad grupo (AG) o conmutación por error (FCI) abarca más de un sitio, cada sitio normalmente tiene su propia red. A menudo, esto significa que cada sitio tiene su propia asignación de direcciones IP. Por ejemplo, direcciones de sitio del empiezan por 192.168.1. *x* e iniciar las direcciones del sitio B con 192.168.2. *x*, donde *x* es la parte de la dirección IP que sea única en el servidor. Sin algún tipo de enrutamiento en el lugar en el nivel de red, estos servidores no podrán comunicarse entre sí. Hay dos formas de controlar este escenario: configurar una red que relaciona las dos subredes diferentes, conocidas como una VLAN, o configure el enrutamiento entre las subredes.

## <a name="vlan-based-solution"></a>Solución basada en VLAN
 
**Requisitos previos**: solución para una VLAN, cada servidor que participe en un AG o FCI necesita dos tarjetas de red (NIC) para una disponibilidad adecuada (un NIC de doble puerto sería un único punto de error en un servidor físico), por lo que se pueden asignar direcciones IP en la subred nativo, así como uno de la VLAN. Esto es además de otras necesidades de red, como iSCSI, que también tiene su propia red.

La creación de la dirección IP para el AG o FCI se realiza en la VLAN. En el ejemplo siguiente, la VLAN tiene una subred de 192.168.3. *x*, por lo que la dirección IP creada para el AG o FCI es 192.168.3.104. Ninguna acción adicional debe configurarse, ya que no hay una única dirección IP asignada al AG o FCI.

![](./media/sql-server-linux-configure-multiple-subnet/image1.png)

## <a name="configuration-with-pacemaker"></a>Configuración con marcapasos

En el mundo de Windows, un clúster de conmutación por error de Windows Server (WSFC) de forma nativa es compatible con varias subredes y controla varias direcciones IP a través de una dependencia OR en la dirección IP. En Linux, no hay ninguna dependencia OR, pero no hay una manera de lograr una correcta múltiples subredes de forma nativa con marcapasos, como se muestra en el siguiente. No se puede hacer esto simplemente utilizando la línea de comandos marcapasos normal para modificar un recurso. Debe modificar la información de clúster base (CIB). El CIB es un archivo XML con la configuración de marcapasos.

![](./media/sql-server-linux-configure-multiple-subnet/image2.png)

### <a name="update-the-cib"></a>Actualizar el CIB

1.  Exportar el CIB.

    **Red Hat Enterprise Linux (RHEL) y Ubuntu**

    ```bash
    sudo pcs cluster cib <filename>
    ```

    **SUSE Linux Enterprise Server (SLES)**

    ```bash
    sudo cibadmin -Q > <filename>
    ```

    Donde *filename* es el nombre que desea llamar el CIB.

2.  Edite el archivo que se generó. Busque la `<resources>` sección. Verá los distintos recursos que se crearon para el AG o FCI. Encuentre el asociado con la dirección IP. Agregar un `<instance attributes>` sección con la información de la segunda dirección IP por encima o debajo de la existente, pero antes `<operations>`. Es similar a la sintaxis siguiente:

    ```xml
    <instance attributes id="<NameForAttribute>" score="<Score>">
        <rule id="<RuleName>" score="INFINITY">
            <expression id="<ExpressionName>" attribute="\#uname" operation="eq" value="<NodeNameInSubnet2>" />
        </rule>
        <nvpair id="<NameForSecondIP>" name="ip" value="<IPAddress>"/>
        <nvpair id="<NameForSecondIPNetmask>" name="cidr\_netmask" value="<Netmask>"/>
    </instance attributes>
    ```
    
    donde *NameForAttribute* es el nombre único para este atributo, *puntuación* es el número asignado al atributo, que debe ser mayor que la subred principal, *RuleName*es el nombre de la regla de *ExpressionName* es el nombre de la expresión, *NodeNameInSubnet2* es el nombre del nodo en el resto de subredes, *NameForSecondIP* es el nombre asociado a la segunda dirección IP, *IPAddress* es la dirección IP para la segunda subred *NameForSecondIPNetmask* es el nombre asociado con la máscara de red, y *Máscara de red* es la máscara de red para la segunda subred.
    
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

3.  Importe el CIB modificado y volver a configurar a marcapasos.

    **RHEL/Ubuntu**
    
    ```bash
    sudo pcs cluster cib-push <filename>
    ```

    **SLES GRANDE**
    
    ```bash
    sudo cibadmin -R -x <filename>
    ```

    donde *filename* es el nombre del archivo CIB con la información de dirección IP modificada.

### <a name="check-and-verify-failover"></a>Compruebe y conmutación por error

1.  Después de que se ha aplicado correctamente la CIB con la configuración actualizada, haga ping al nombre DNS asociado al recurso de dirección IP en marcapasos. Debe reflejar la dirección IP asociada a la subred que hospeda actualmente la AG o FCI.
2.  Producirá un error en el AG o FCI para el resto de las subredes.
3.  Después de que el AG o FCI está totalmente en línea, haga ping en el nombre DNS asociado con la dirección IP. Debe reflejar la dirección IP en la segunda subred.
4.  Si lo desea, el AG o FCI conmuten por recuperación a la subred original.
