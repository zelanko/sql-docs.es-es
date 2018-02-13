---
title: "Conceptos básicos de la disponibilidad de SQL Server para las implementaciones de Linux | Documentos de Microsoft"
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: On Demand
ms.openlocfilehash: fd2079b0b0186192fc3b55e7a6ccefd25c1a46bc
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Conceptos básicos de la disponibilidad de SQL Server para las implementaciones de Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

A partir de [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] es compatible con Linux y Windows. Basado en Windows, como [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] las implementaciones, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] las bases de datos e instancias deben estar altamente disponible en Linux. Este artículo tratan los aspectos técnicos de planificación e implementación de alta disponibilidad basadas en Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] bases de datos e instancias, así como algunas de las diferencias de las instalaciones basadas en Windows. Dado que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] puede ser nuevo para profesionales de TI de Linux y Linux pueden ser nuevo para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] profesionales de TI, el artículo a veces presenta conceptos que pueden ser poco familiar para otros usuarios y familiar a algunas.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]Opciones de disponibilidad para las implementaciones de Linux
Además de la copia de seguridad y restauración, las mismas tres características de disponibilidad están disponibles en Linux que para las implementaciones basadas en Windows:
-   Grupos de disponibilidad AlwaysOn (AG)
-   Siempre en instancias de clúster de conmutación por error (FCI)
-   [Trasvase de registros](sql-server-linux-use-log-shipping.md)

En Windows, fci siempre requiere un clúster de conmutación por error de Windows Server (WSFC) subyacente. Según el escenario de implementación, un AG normalmente requiere un WSFC subyacente, con la excepción que se va a la nueva ninguno variant en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. No existe un WSFC en Linux. Implementación de Linux de agrupación en clústeres se describe en la sección [marcapasos para clúster de conmutación por error y grupos de disponibilidad AlwaysOn instancias en Linux](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux).

## <a name="a-quick-linux-primer"></a>Texto elemental sobre Linux rápido
Aunque algunas instalaciones de Linux pueden instalarse con una interfaz, la mayoría son no es así, lo que significa que casi todo en el nivel de sistema operativo se realiza a través de la línea de comandos. El término común para esta línea de comandos en el mundo de Linux es un *shell de bash*.

En Linux, muchos comandos tienen que ejecutarse con privilegios elevados, igual muchas cosas tienen que realizarse en Windows Server como administrador. Hay dos métodos principales para ejecutar con privilegios elevados:
1. Ejecutar en el contexto del usuario apropiado. Para cambiar a otro usuario, use el comando `su`. Si `su` se ejecuta en su propio sin un nombre de usuario, siempre y cuando conozca la contraseña, ahora estará en un shell como *raíz*.
   
2. La más común y seguridad consciente forma ejecutar cosas es usar `sudo` antes de ejecutar cualquier cosa. Muchos de los ejemplos de este artículo utilizan `sudo`.

Algunos comandos comunes, cada uno de los cuales tienen diversos modificadores y opciones que se pueden investigar en línea:
-   `cd`: cambiar el directorio
-   `chmod`: cambiar los permisos de un archivo o directorio
-   `chown`: cambiar la propiedad de un archivo o directorio
-   `ls`: mostrar el contenido de un directorio
-   `mkdir`: cree una carpeta (directorio) en una unidad
-   `mv`: mover un archivo de una ubicación a otra
-   `ps`: mostrar todos los procesos de trabajo
-   `rm`: elimina un archivo localmente en un servidor
-   `rmdir`: eliminar una carpeta (directorio)
-   `systemctl`: iniciar, detener o habilitar los servicios
-   Comandos del editor de texto. En Linux, hay varias opciones del editor de texto, como vi y emacs.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Tareas comunes para las configuraciones de disponibilidad de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux
En esta sección se trata las tareas que son comunes a todos los basados en Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] las implementaciones.

### <a name="ensure-that-files-can-be-copied"></a>Asegúrese de que se pueden copiar los archivos
Copiar archivos desde un servidor a otro es una tarea que cualquier usuario con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, debe ser capaz de hacer. Esta tarea es muy importante para las configuraciones de AG.

Cosas como problemas de permisos pueden existir en Linux, así como en las instalaciones basadas en Windows. Sin embargo, aquellos que estén familiarizados con la copia de un servidor a otro en Windows pueden no estar familiarizados con cómo se hizo en Linux. Un método común consiste en usar la utilidad de línea de comandos `scp`, que es el acrónimo copia seguro. En segundo plano, `scp` usa OpenSSH. SSH es el acrónimo shell seguro. Dependiendo de la distribución de Linux, puede que no estén instalado OpenSSH propio. Si no es así, OpenSSH debe instalarse primero. Para obtener más información acerca de cómo configurar OpenSSH, consulte la información en los siguientes vínculos para cada distribución:
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Al utilizar `scp`, debe proporcionar las credenciales del servidor si no es el origen o destino. Por ejemplo, si se usa

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

copia el archivo MyAGCert.cer en la carpeta especificada en el otro servidor. Tenga en cuenta que debe tener permisos: y, posiblemente, – la titularidad del archivo para copiarlo y, por lo que `chown` que también necesite emplearse antes de copiar. De forma similar, en el lado receptor, el usuario necesita acceso para manipular el archivo. Por ejemplo, para restaurar ese archivo de certificado, la `mssql` usuario debe poder tener acceso a él.

Samba, que es la variante de Linux de bloque de mensajes del servidor (SMB), también puede utilizarse para crear recursos compartidos de acceso a las rutas de acceso UNC, como `\\SERVERNAME\SHARE`. Para obtener más información acerca de cómo configurar Samba, consulte la información en los siguientes vínculos para cada distribución:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

También se pueden utilizar recursos compartidos SMB basado en Windows; Recursos compartidos de SMB no necesitan estar basada en Linux, siempre y cuando la parte de cliente de Samba está configurada correctamente en el servidor que hospeda Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] y el recurso compartido no tiene derechos de acceso. Para los miembros de un entorno mixto, esto sería una forma de aprovechar la infraestructura existente para Linux-based [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] las implementaciones.

Único lo que es importante es que la versión de Samba implementado debe ser compatible de SMB 3.0. Cuando se agregó compatibilidad con SMB en [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], era necesario que todos los recursos compartidos para admitir SMB 3.0. Si usa Samba para el recurso compartido y no a Windows Server, el recurso compartido de Samba debería estar utilizando Samba 4.0 o posterior y lo ideal es que 4.3 o posterior, que es compatible con SMB 3.1.1. Es una buena fuente de información acerca de SMB y Linux [SMB3 en Samba](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf).

Por último, el uso de un recurso compartido de red archivos system (NFS) es una opción. Uso de NFS no es una opción en implementaciones basadas en Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]y solo pueden usarse en las implementaciones basadas en Linux.

### <a name="configure-the-firewall"></a>Configuración del firewall
Las distribuciones de Linux similar a Windows, tienen un firewall integrado. Si su empresa usa un firewall externo a los servidores, la deshabilitación de los firewalls en Linux puede ser aceptable. Sin embargo, independientemente de que el firewall está habilitado, hay puertos que se abran. En la tabla siguiente se documenta los puertos comunes necesarios para alta disponibilidad [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implementaciones en Linux.

| Número de puerto | Tipo     | Description                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS:`rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (si se usan): asignador de puntos finales                                                                                          |
| 137         | UDP      | Samba (si se usan): servicio de nombres NetBIOS                                                                                      |
| 138         | UDP      | Samba (si se usan): datagrama NetBIOS                                                                                          |
| 139         | TCP      | Samba (si se usan): sesión de NetBIOS                                                                                           |
| 445         | TCP      | Samba (si se usan): SMB a través de TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] –; el puerto predeterminado Si lo desea, puede cambiar con`mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (si se usa)                                                                                                               |
| 2224        | TCP      | Marcapasos – utilizados por`pcsd`                                                                                                |
| 3121        | TCP      | Marcapasos: necesario si hay nodos marcapasos remotos                                                                    |
| 3260        | TCP      | iSCSI del iniciador (si se usan): se puede modificar en `/etc/iscsi/iscsid.config` (RHEL), pero debe coincidir con el puerto de destino iSCSI |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -usa para un extremo AG; el puerto predeterminado se puede cambiar al crear el punto de conexión                                |
| 5403        | TCP      | Marcapasos                                                                                                                   |
| 5404        | UDP      | Marcapasos – requerido Corosync si usa multidifusión UDP                                                                     |
| 5405        | UDP      | Marcapasos: requeridos por Corosync                                                                                            |
| 21064       | TCP      | Marcapasos – requerido recursos usando DLM                                                                                 |
| Variable    | TCP      | Puerto de extremo AG; valor predeterminado es 5022                                                                                           |
| Variable    | TCP      | Puerto de NFS: para `LOCKD_TCPPORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL)                                              |
| Variable    | UDP      | Puerto de NFS: para `LOCKD_UDPPORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL)                                              |
| Variable    | TCP/UDP  | Puerto de NFS: para `MOUNTD_PORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL)                                                |
| Variable    | TCP/UDP  | Puerto de NFS: para `STATD_PORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL)                                                 |

Para puertos adicionales que pueden utilizarse por Samba, consulte [uso del puerto Samba](https://wiki.samba.org/index.php/Samba_Port_Usage).

Por el contrario, el nombre del servicio en Linux también puede agregarse como una excepción en lugar del puerto; Por ejemplo, `high-availability` para marcapasos. Hacer referencia a la distribución de los nombres si esta es la dirección que se va a seguir. Por ejemplo, en RHEL es el comando para agregar en marcapasos

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**Documentación del firewall:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>Instalar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] paquetes de disponibilidad
En basado en Windows [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instalación, algunos componentes se instalan incluso en una instalación de motor básico, mientras que otros no lo están. En Linux, solo el [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] motor se instala como parte del proceso de instalación. Todo lo demás es opcional. Para alta disponibilidad [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instancias en Linux, se deben instalar dos paquetes con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente (*agente de server mssql*) y el paquete de alta disponibilidad (HA) ( *MSSQL-server-ha*). Mientras [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente es técnicamente opcional, se [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]del programador de trabajos y es obligatorio para el trasvase de registros, por lo que se recomienda la instalación. En las instalaciones basadas en Windows, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente no es opcional.

>[!NOTE]
>Para los nuevos a [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]del programador de trabajos integradas. Es una forma común para los DBA programar acciones como las copias de seguridad y otros [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] mantenimiento. A diferencia de una instalación basada en Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] donde [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente es un servicio completamente diferente, en Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente se ejecuta en el contexto de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] propio.

Cuando se configura grupos de disponibilidad o fci en una configuración basada en Windows, son compatibles con clústeres. Compatibilidad con clústeres significa que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] tiene el recurso específico de archivos DLL que conoce un WSFC (sqagtres.dll y sqsrvres.dll para fci, hadrres.dll para grupos de disponibilidad) y se usan por el WSFC para asegurarse de que la [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] funcionalidad clúster está activo, ejecutando, y funciona correctamente. Dado de agrupación en clústeres es externo no solo a [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pero Linux propio, Microsoft tenía codificar el equivalente de una DLL de recursos para las implementaciones basadas en Linux AG y FCI. Se trata de la *mssql-server-ha* del paquete, también conocido como el [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente de recursos para marcapasos. Para instalar el *mssql-server-ha* del paquete, consulte [instalar los paquetes de alta disponibilidad y Agente SQL Server](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages).

Los otros paquetes opcionales para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Full-Text Search (*mssql-server-FT*) y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql servidor es*), no son es necesario para lograr alta disponibilidad, para ver si una FCI o un AG.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Marcapasos para instancias de clúster de conmutación por error en Linux y grupos de disponibilidad AlwaysOn
Anterior como se indicó, el único mecanismo de agrupación en clústeres admitido actualmente por Microsoft para grupos de disponibilidad y fci es marcapasos con Corosync. Esta sección ofrece la información básica para entender la solución, así como cómo planear e implementar para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] configuraciones.

### <a name="ha-add-onextension-basics"></a>Conceptos básicos de complemento en/extensión de alta disponibilidad
Todas las distribuciones compatibles actualmente incluyen una alta disponibilidad complemento-on/extensión, que se basa en la pila de agrupación en clústeres de marcapasos. Esta pila incorpora dos componentes clave: marcapasos y Corosync. Todos los componentes de la pila son:
-   Marcapasos: el núcleo del componente, que lleva a cabo acciones como coordenadas en los equipos en clúster de agrupación en clústeres.
-   Corosync: un marco y conjunto de API que proporciona elementos tales como el quórum, la capacidad de procesos no se puede reiniciar y así sucesivamente.
-   libQB – proporciona cosas como el registro.
-   Agente de recursos: funcionalidad específica que proporciona para que una aplicación puede integrar con marcapasos.
-   Valla de agente de secuencias de comandos o funcionalidad que ayudarte a aislar los nodos y tratarlos si están teniendo problemas.
    
> [!NOTE]
> La pila de clúster se conoce normalmente como marcapasos en el mundo de Linux.

Esta solución es en cierta forma es similar a, pero en muchos aspectos diferentes de la implementación de las configuraciones en clúster con Windows. En Windows, la forma de disponibilidad de agrupación en clústeres, llama a un clúster de conmutación por error de Windows Server (WSFC), está integrada en el sistema operativo y la característica que permite la creación de un WSFC, agrupación en clústeres de conmutación por error, está deshabilitada de forma predeterminada. En Windows, grupos de disponibilidad y fci se crean sobre un WSFC y compartir una estrecha integración debido a la DLL que se proporciona por de recursos específico [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Esta solución acoplada estrechamente con diferencia es posible porque es todo ello desde un proveedor.

![](./media/sql-server-linux-ha-basics/image1.png)

En Linux, mientras que cada distribución admitido tiene marcapasos disponibles, cada distribución puede personalizar y tener versiones y ligeramente distintas implementaciones. Algunas de las diferencias se verán reflejados en las instrucciones de este artículo. El nivel de agrupación en clústeres es código abierto, por lo que aunque se distribuye con las distribuciones, no está estrechamente integrado en la misma forma un WSFC está por debajo de Windows. Por lo tanto, Microsoft proporciona *mssql-server-ha*, de modo que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] y la pila marcapasos puede proporcionar cerca, pero no es exactamente la misma experiencia para grupos de disponibilidad y fci en Windows.

Para obtener documentación completa sobre marcapasos, incluida una explicación más detallada de todo el contenido es con información de referencia completa, para RHEL y SLES:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu no tiene una guía para la disponibilidad.

Para obtener más información acerca de la pila completa, consulte también el oficial [página de documentación de marcapasos](http://clusterlabs.org/doc/) en el sitio Clusterlabs.

### <a name="pacemaker-concepts-and-terminology"></a>Marcapasos conceptos y terminología
Esta sección describe los conceptos y terminología de una implementación marcapasos comunes.

#### <a name="node"></a>Nodo
Un nodo es un servidor que participan en el clúster. Un clúster marcapasos admite hasta 16 nodos de forma nativa. Este número se puede superar si Corosync no se está ejecutando en los nodos adicionales, pero es necesario para Corosync [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Por lo tanto, el número máximo de nodos de un clúster puede tener cualquiera [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-configuración según es 16; lo es el límite de marcapasos y no tiene nada que ver con las limitaciones de máximas de grupos de disponibilidad o fci impuestas por [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. 

#### <a name="resource"></a>Recurso
Un WSFC y un clúster marcapasos tienen el concepto de un recurso. Un recurso es una funcionalidad específica que se ejecuta en el contexto del clúster, como un disco o una dirección IP. Por ejemplo, en marcapasos obtener pueden crear recursos de FCI y AG. Esto no es diferente a lo que se realiza en un WSFC, donde verá un [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] recurso para ser una FCI o un grupo de disponibilidad al configurar un grupo de disponibilidad pero no es exactamente el mismo debido a las diferencias en cómo subyacentes [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] se integra con marcapasos.

Marcapasos tiene recursos estándar y el clon. Clon recursos son los que se ejecutan simultáneamente en todos los nodos. Un ejemplo sería una dirección IP que se ejecuta en varios nodos para equilibrar la carga. Cualquier recurso que se crea para fci usa un recurso estándar, ya que sólo un nodo puede alojar una FCI en cualquier momento.

Cuando se crea un AG, requiere una forma especializada de un recurso de clon llamado a un recurso de varios estado. Mientras un AG sólo tiene una réplica principal, el valor de AG. se está ejecutando en todos los nodos que se configura para que funcionen en y pueden permitir potencialmente cosas como el acceso de solo lectura. Dado que se trata de un uso "activo" del nodo, los recursos que tienen el concepto de dos estados: principal y secundario. Para obtener más información, consulte [varios Estados recursos: recursos que tienen varios modos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html).

#### <a name="resource-groupssets"></a>Conjunto de grupos de recursos
Similares a los roles en un WSFC, un clúster marcapasos tiene el concepto de un grupo de recursos. Un grupo de recursos (denominado un conjunto en SLES) es una colección de recursos que funcionan juntos y puede conmutar por error de un nodo a otro como una sola unidad. Grupos de recursos no pueden contener recursos que están configurados como maestro/esclavo; por lo tanto, no se puede usar para grupos de disponibilidad. Mientras que un grupo de recursos puede utilizarse para fci, no es generalmente una configuración recomendada.

#### <a name="constraints"></a>Restricciones
WSFCs tiene varios parámetros para los recursos, así como aspectos como dependencias, que indican el WSFC de una relación de elemento primario/secundario entre dos recursos distintos. Una dependencia es simplemente una regla que se lo indica el WSFC qué recursos deben estar en línea en primer lugar.

Un clúster marcapasos no tiene el concepto de dependencias, pero existen restricciones. Hay tres tipos de restricciones: la colocación, la ubicación y la ordenación.
-   Una restricción de colocación exige o no deben disponer de dos recursos en el mismo nodo.
-   Una restricción de ubicación indica al clúster de marcapasos donde ejecutar un recurso puede (o no).
-   Una restricción de ordenación indica al clúster de marcapasos el orden en que deberían empezar a los recursos.

> [!NOTE]
> Las restricciones de colocación no son necesarias para los recursos en un grupo de recursos, ya que todas aquellas que se ven como una sola unidad.

#### <a name="quorum-fence-agents-and-stonith"></a>Quórum, los agentes de barrera y STONITH
Quórum en marcapasos es similar a un WSFC en su concepto. La principal finalidad de mecanismo de quórum del clúster es asegurarse de que el clúster permanece activados y ejecutándose. Los complementos de alta disponibilidad para las distribuciones de Linux y un WSFC tienen el concepto de votación, donde cada nodo se cuenta en quórum. Desea una mayoría de los votos, de lo contrario, en un escenario de caso peor, dejará de estar disponible el clúster.

A diferencia de un WSFC, no hay ningún recurso de testigo para trabajar con quórum. Al igual que un WSFC, el objetivo es mantener el número de electores impares. Configuración de quórum tiene diferentes consideraciones para grupos de disponibilidad que fci.

WSFCs supervisar el estado de los nodos que participan y controlarlos cuando se produce un problema. Las versiones posteriores de WSFCs ofrecen características tales como poner en cuarentena un nodo que esté disponible o que (nodo no está activado, la comunicación de red es hacia abajo, etcetera). En el lado de Linux, este tipo de funcionalidad se proporciona un agente de barrera. El concepto se conoce a veces como barrera. Sin embargo, estos agentes de barrera son generalmente específicos de la implementación y a menudo proporcionan por los proveedores de hardware y algunos proveedores de software, como aquellos que proporcionan los hipervisores. Por ejemplo, VMware proporciona a un agente de barrera que puede usarse para máquinas virtuales de Linux que se virtualizan mediante vSphere.

Quórum y vínculos de barrera en otro concepto denominado STONITH o grabar el otro nodo en el encabezado. STONITH debe tener un clúster marcapasos compatibles en todas las distribuciones de Linux. Para obtener más información, consulte [de barrera en un clúster de disponibilidad alta de Red Hat](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
El `corosync.conf` archivo contiene la configuración del clúster. Se encuentra en `/etc/corosync`. En el curso de las operaciones diarias normales, este archivo nunca debería tener que se puede editar si el clúster está configurado correctamente.

#### <a name="cluster-log-location"></a>Ubicación del registro de clúster
Ubicaciones de registro para los clústeres de marcapasos varían según la distribución.
-   RHEL y SLES-`/var/log/cluster/corosync.log`
-   Ubuntu:`/var/log/corosync/corosync.log`

Para cambiar la ubicación de registro de forma predeterminada, modifique `corosync.conf`.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Plan marcapasos clústeres para[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Esta sección describen los puntos de planeación importantes para un clúster marcapasos.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Para los clústeres de virtualización marcapasos basados en Linux[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Uso de máquinas virtuales para implementar basados en Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] las implementaciones de grupos de disponibilidad y fci está cubierto por las mismas reglas que sus homólogos basados en Windows. Hay un conjunto básico de reglas para la compatibilidad de virtualizado [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implementaciones proporcionadas por Microsoft en [956893 de KB de soporte técnico de Microsoft](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment). Hipervisores diferentes, como los Hyper-V de Microsoft y VMware ESXi pueden tener diferentes variaciones en el mismo, debido a diferencias en las plataformas a sí mismos.

En cuanto a grupos de disponibilidad y fci en virtualización, asegúrese de que antiafinidad se establece para los nodos de un determinado clúster marcapasos. Cuando se configura para alta disponibilidad en una configuración AG o FCI, las máquinas virtuales de hospedaje [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] nunca debe ejecutarse en el mismo host del hipervisor. Por ejemplo, si se implementa una FCI de dos nodos, se debe haber *al menos* tres hosts de hipervisor por lo que existe en algún lugar de una de las máquinas virtuales que hospeda un nodo para ir si se produce un error del host, especialmente si usa características como Live La migración o vMotion.

Para obtener más detalles, consulte:
-   Documentación de Hyper-V – [usar clústeres invitados para alta disponibilidad](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   Notas del producto (se escribe para las implementaciones basadas en Windows, pero la mayoría de los conceptos que todavía se aplican): [planeación de alta disponibilidad, de misión crítica implementaciones de SQL Server con VMware vSphere](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>RHEL con un clúster marcapasos con STONITH no es compatible todavía con Hyper-V. Hasta que se admite para obtener más información y las actualizaciones, consulte [directivas de soporte técnico para los clústeres de disponibilidad alta de RHEL](https://access.redhat.com/articles/29440#3physical_host_mixing).

### <a name="networking"></a>Redes
A diferencia de un WSFC marcapasos no requieren un nombre dedicado o al menos una dirección IP dedicada para el propio clúster marcapasos. Grupos de disponibilidad y fci requerirá direcciones IP (consulte la documentación de cada uno de ellos para obtener más información), pero no nombres, dado que no hay ningún recurso de nombre de red. SLES permiten la configuración de una dirección IP con fines de administración, pero no es necesario, tal y como se aprecia en [crear el clúster marcapasos](sql-server-linux-deploy-pacemaker-cluster.md#create).

Al igual que un WSFC marcapasos sería preferible redes redundantes, lo que significa que las tarjetas de red distintos (NIC o pNICs para física) con las direcciones IP individuales. En cuanto a la configuración del clúster, cada dirección IP tendría lo que se conoce como su propio anillo. Sin embargo, como con WSFCs hoy en día, se virtualizan muchas implementaciones o en la nube pública que realmente no hay sólo un único virtualiza NIC (vNIC) que se muestre en el servidor. Si todos los pNICs y vNICs están conectados al mismo conmutador físico o virtual, no hay redundancia true en el nivel de red, por lo que la configuración de varias NIC es un poco de en realidad a la máquina virtual. Redundancia de red normalmente se integra en el hipervisor para implementaciones virtualizadas y definitivamente está integrada en la nube pública.

Una diferencia con varias NIC y marcapasos frente a un WSFC es que marcapasos permite varias direcciones IP en la misma subred, mientras que un WSFC no lo hace. Para obtener más información sobre varias subredes y clústeres de Linux, vea el artículo [configurar varias subredes](sql-server-linux-configure-multiple-subnet.md).

### <a name="quorum-and-stonith"></a>Quórum y STONITH
Configuración de quórum y los requisitos están relacionados con las implementaciones de AG o específicas de FCI de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

STONITH es necesaria para un clúster marcapasos compatibles. Use la documentación de la distribución para configurar STONITH. Un ejemplo es en [basado en almacenamiento barrera](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) para SLES. También hay un agente STONITH para VMware vCenter para soluciones basadas en ESXI. Para obtener más información, consulte [Stonith complemento agente de barrera de VMWare virtual VCenter SOAP (Unofficial)](https://github.com/olafrv/fence_vmware_soap).

> [!NOTE]
> Al redactar este artículo, Hyper-V no tiene una solución para STONITH. Esto es cierto para en las implementaciones locales y también afecta a las implementaciones de marcapasos basado en Azure con ciertas distribuciones como RHEL.

### <a name="interoperability"></a>Interoperabilidad
Esta sección describe cómo un clúster basado en Linux puede interactuar con un WSFC o con otras distribuciones de Linux.

#### <a name="wsfc"></a>WSFC
Actualmente, no hay ninguna manera directa de un WSFC y un clúster marcapasos trabajen juntos. Esto significa que no hay ninguna manera de crear un AG o FCI que funciona a través de un clúster WSFC y marcapasos. Sin embargo, hay dos soluciones de interoperabilidad, ambos de los cuales están diseñados para grupos de disponibilidad. La única forma de que una FCI puede participar en una configuración de plataforma cruzada es si se participa como una instancia de uno de estos dos escenarios:
-   Un AG con un tipo de clúster de None. Para obtener más información, consulte las ventanas [documentación de grupos de disponibilidad](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).
-   AG distribuida, que es un tipo especial de grupo de disponibilidad que permite a dos grupos de disponibilidad diferentes para configurarse como su propio grupo de disponibilidad. Para obtener más información sobre grupos de disponibilidad distribuidos, consulte la documentación [grupos de disponibilidad distribuidos](../database-engine/availability-groups/windows/distributed-availability-groups.md).

#### <a name="other-linux-distributions"></a>Otras distribuciones de Linux
En Linux, todos los nodos de un clúster marcapasos deben estar en la misma distribución. Por ejemplo, esto significa que un nodo RHEL no puede formar parte de un clúster marcapasos que tiene un nodo SLES. La razón principal para esto se indicados anteriormente: las distribuciones pueden tener distintas versiones y funcionalidad, para cosas no pudieran funcione correctamente. Combinación de distribuciones tiene el mismo artículo que mezclar WSFCs y Linux: utilizamos ninguno o grupos de disponibilidad está distribuido.

## <a name="next-steps"></a>Pasos siguientes
[Implementar un clúster marcapasos para SQL Server en Linux](sql-server-linux-deploy-pacemaker-cluster.md)
