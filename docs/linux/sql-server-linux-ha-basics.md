---
title: Alta disponibilidad de SQL Server en implementaciones de Linux
description: Obtenga información sobre las diferentes opciones de alta disponibilidad que existen para SQL Server en Linux, como los grupos de disponibilidad AlwaysOn, las instancias de clúster de conmutación por error (FCI) y el trasvase de registros.
ms.custom: seo-lt-2019
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 474533a69d74512e3e305f44d96f90009aa64e00
ms.sourcegitcommit: 34d28d49e8d0910cf06efda686e2d73059569bf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/04/2020
ms.locfileid: "75656615"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Conceptos básicos sobre disponibilidad de SQL Server en implementaciones de Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

A partir de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[sssql17-md](../includes/sssql17-md.md)] se admite en Linux y en Windows. Al igual que las implementaciones basadas en Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], las bases de datos y las instancias de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] deben tener una alta disponibilidad en Linux. En este artículo se abordan los aspectos técnicos de la planeación e implementación de bases de datos e instancias de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basadas en Linux de alta disponibilidad, así como algunas de las diferencias con respecto a las instalaciones basadas en Windows. Como [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] puede ser una novedad para los profesionales de Linux, así como Linux para los profesionales de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], el artículo a veces reflejará conceptos que pueden ser familiares para algunos y desconocidos para otros.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>Opciones de disponibilidad de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en implementaciones de Linux
Aparte de las copias de seguridad y la restauración, las mismas tres características de disponibilidad están presentes en las implementaciones basadas tanto en Linux como en Windows:
-   Grupos de disponibilidad AlwaysOn
-   Instancias de clúster de conmutación por error de AlwaysOn
-   [Trasvase de registros](sql-server-linux-use-log-shipping.md)

En Windows, las instancias de clúster de conmutación por error requieren un clúster de conmutación por error de Windows Server (WSFC) subyacente. Dependiendo del escenario de implementación, un grupo de disponibilidad suele requerir un WSFC subyacente, con la excepción de la nueva variante None en [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. En Linux no hay un WSFC. La implementación en clúster en Linux se describe en la sección [Pacemaker para grupos de disponibilidad e instancias de clúster de conmutación por error de AlwaysOn en Linux](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux).

## <a name="a-quick-linux-primer"></a>Manual rápido de Linux
Aunque algunas instalaciones de Linux se pueden instalar con una interfaz, la mayoría no lo hacen, lo que significa que casi todo lo que hay en la capa del sistema operativo se realiza a través de la línea de comandos. El término común para esta línea de comandos en el mundo Linux es *shell Bash*.

En Linux, muchos comandos se deben ejecutar con privilegios elevados, de forma muy parecida a como haría un administrador en Windows Server. Hay dos métodos principales para ejecutar acciones con privilegios elevados:
1. Realizar la ejecución en el contexto del usuario adecuado. Para cambiar a otro usuario, use el comando `su`. Si `su` se ejecuta por sí solo sin un nombre de usuario, y siempre y cuando conozca la contraseña, estará en un shell como *raíz*.
   
2. La forma más común y basada en la seguridad de ejecutar acciones es usar `sudo` antes de ejecutar nada. En muchos de los ejemplos de este artículo se usa `sudo`.

Estos son algunos comandos comunes; todos ellos tienen varios modificadores y opciones que se pueden investigar en línea:
-   `cd`: sirve para cambiar de directorio.
-   `chmod`: sirve para cambiar los permisos de un archivo o un directorio.
-   `chown`: sirve para cambiar la propiedad de un archivo o un directorio.
-   `ls`: sirve para mostrar el contenido de un directorio.
-   `mkdir`: sirve para crear una carpeta (directorio) en una unidad.
-   `mv`: sirve para mover un archivo de una ubicación a otra.
-   `ps`: sirve para mostrar todos los procesos en funcionamiento.
-   `rm`: sirve para eliminar un archivo localmente en un servidor.
-   `rmdir`: sirve para eliminar una carpeta (directorio).
-   `systemctl`: sirve para iniciar, detener o habilitar servicios.
-   Comandos del editor de texto. En Linux hay varias opciones del editor de texto, como vi y emacs.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Tareas comunes para configurar la disponibilidad de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux
En esta sección se describen las tareas comunes a todas las implementaciones de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basadas en Linux.

### <a name="ensure-that-files-can-be-copied"></a>Garantizar que los archivos se pueden copiar
Copiar archivos de un servidor a otro es una tarea que cualquier persona que use [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux debería poder realizar. Esta tarea es muy importante para las configuraciones de grupos de disponibilidad.

Pueden surgir cuestiones como problemas de permisos en las instalaciones basadas tanto en Linux como en Windows. Sin embargo, es posible que los usuarios familiarizados con copiar de un servidor a otro en Windows no sepan cómo hacerlo en Linux. Un método común es usar la utilidad de la línea de comandos `scp`, que significa "copia segura". En segundo plano, `scp` usa OpenSSH. SSH significa "shell seguro". En función de la distribución de Linux, es posible que OpenSSH no esté instalado de por sí. Si no lo está, OpenSSH debe instalarse primero. Para más información sobre cómo configurar OpenSSH, vea los siguientes vínculos relativos a cada distribución:
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/deployment_guide/ch-openssh)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Al usar `scp`, debe proporcionar las credenciales del servidor si no es el origen o el destino. Por ejemplo, si se usa

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

el archivo MyAGCert.cer se copia en la carpeta especificada en el otro servidor. Tenga en cuenta que debe tener permisos en el archivo (y, posiblemente, ser el propietario de este) para copiarlo, con lo cual es posible que deba usar también `chown` antes de copiar. Del mismo modo, en el lado receptor, el usuario adecuado necesita acceso para manipular el archivo. Por ejemplo, para restaurar ese archivo de certificado, el usuario de `mssql` debe poder acceder a él.

También se puede usar Samba, que es la variante de Linux del Bloque de mensajes del servidor (SMB), para crear recursos compartidos a los que acceden las rutas de acceso UNC como `\\SERVERNAME\SHARE`. Para más información sobre cómo configurar Samba, vea los siguientes vínculos relativos a cada distribución:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

También se pueden usar recursos compartidos de SMB basados en Windows; no es necesario que los recursos compartidos de SMB estén basados en Linux, siempre y cuando la parte del cliente de Samba esté configurada correctamente en el servidor Linux que hospeda [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] y el recurso compartido tenga el acceso adecuado. En el caso de los entornos mixtos, esto sería una manera de aprovechar la infraestructura existente para las implementaciones de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basadas en Linux.

Algo importante es que la versión de Samba implementada debe ser compatible con SMB 3.0. Cuando se agregó compatibilidad con SMB en [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], era necesario que todos los recursos compartidos admitieran SMB 3.0. Si se usa Samba para el recurso compartido y no Windows Server, dicho recurso compartido basado en Samba debe usar Samba 4.0 o posterior e, idealmente, la versión 4.3 o posterior, que admite SMB 3.1.1. Una buena fuente de información sobre SMB y Linux es [SMB3 en Samba](https://events.static.linuxfound.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf).

Por último, usar un recurso compartido de Network File System (NFS) es una opción. El uso de NFS no es una opción en las implementaciones de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basadas en Windows; solo se puede usar en implementaciones basadas en Linux.

### <a name="configure-the-firewall"></a>Configuración del firewall
De forma similar a Windows, las distribuciones de Linux tienen un firewall integrado. Si en su empresa se usa un firewall externo a los servidores, deshabilitar los firewall en Linux es admisible. Sin embargo, independientemente de dónde esté habilitado el firewall, los puertos deben estar abiertos. En la siguiente tabla se documentan los puertos comunes necesarios en implementaciones de alta disponibilidad de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux.

| Número de puerto | Tipo     | Descripción                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS: `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (si se usa): asignador de puntos de conexión                                                                                          |
| 137         | UDP      | Samba (si se usa): servicio de nombres de NetBIOS                                                                                      |
| 138         | UDP      | Samba (si se usa): datagrama de NetBIOS                                                                                          |
| 139         | TCP      | Samba (si se usa): sesión de NetBIOS                                                                                           |
| 445         | TCP      | Samba (si se usa): SMB a través de TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: puerto predeterminado; si lo desea, se puede cambiar por `mssql-conf set network.tcpport <portnumber>`.                       |
| 2049        | TCP, UDP | NFS (si se usa)                                                                                                               |
| 2224        | TCP      | Pacemaker: usado por `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker: indispensable si hay nodos remotos de Pacemaker                                                                    |
| 3260        | TCP      | Iniciador iSCSI (si se usa): se puede modificar en `/etc/iscsi/iscsid.config` (RHEL), pero debe coincidir con el puerto del destino iSCSI. |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: puerto predeterminado usado para un punto de conexión de grupo de disponibilidad; se puede cambiar al crear el punto de conexión.                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker: indispensable para Corosync si se usa un UDP de multidifusión                                                                     |
| 5405        | UDP      | Pacemaker: indispensable para Corosync                                                                                            |
| 21064       | TCP      | Pacemaker: indispensable para los recursos que usan DLM                                                                                 |
| Variable    | TCP      | Puerto del punto de conexión de grupo de disponibilidad; el valor predeterminado es 5022.                                                                                           |
| Variable    | TCP      | NFS: puerto de `LOCKD_TCPPORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL).                                              |
| Variable    | UDP      | NFS: puerto de `LOCKD_UDPPORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL).                                              |
| Variable    | TCP/UDP  | NFS: puerto de `MOUNTD_PORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL).                                                |
| Variable    | TCP/UDP  | NFS: puerto de `STATD_PORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL).                                                 |

Para saber qué otros puertos puede usar Samba, vea [Uso de puertos de Samba](https://wiki.samba.org/index.php/Samba_Port_Usage).

Por otra parte, el nombre del servicio en Linux también se puede agregar como una excepción en lugar del puerto; por ejemplo, `high-availability` para Pacemaker. Consulte su distribución para obtener los nombres si este es el camino que quiere tomar. Por ejemplo, en RHEL, el comando que se agrega en Pacemaker es

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**Documentación del firewall:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>Instalación de paquetes de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para disponibilidad
En una instalación de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basada en Windows, algunos componentes se instalan incluso cuando se trata de una instalación de motor básica, mientras que otros no. En Linux, solo se instala el motor de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] como parte del proceso de instalación. Todo lo demás es opcional. En el caso de las instancias de alta disponibilidad de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, se deben instalar dos paquetes con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: el Agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] (*mssql-server-agent*) y el paquete de alta disponibilidad (*mssql-server-ha*). Aunque el Agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] es opcional desde un punto de vista técnico, es el programador de trabajos de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] y, como tal, es necesario para el trasvase de registros, por lo que se recomienda instalarlo. En las instalaciones basadas en Windows, el Agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] no es opcional.

>[!NOTE]
>Para quienes no conozcan [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], el Agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] es el programador de trabajos integrado de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Es el modo habitual en el que los administradores de bases de datos programan cosas como copias de seguridad y otras tareas de mantenimiento de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. A diferencia de una instalación basada en Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], donde el Agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] es un servicio completamente diferente, en Linux, el Agente [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] se ejecuta en el contexto de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en sí.

Cuando los grupos de disponibilidad o las instancias de clúster de conmutación por error se configuran en una configuración basada en Windows, son compatibles con clústeres. La compatibilidad con clústeres significa que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] tiene archivos DLL de recurso específicos que un WSFC conoce (sqagtres.dll y sqsrvres.dll para las instancias de clúster de conmutación por error; hadrres.dll para los grupos de disponibilidad) y que el WSFC usa para asegurarse de que la funcionalidad de agrupación en clúster de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] funciona y lo hace correctamente. Dado que la agrupación en clústeres es externa no solo por lo que respecta a [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], sino también a Linux, Microsoft tuvo que codificar el equivalente de un archivo DLL de recurso para las implementaciones de grupos de disponibilidad o instancias de clúster de conmutación por error basadas en Linux. Es el paquete *mssql-server-ha*, también conocido como agente de recursos de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para Pacemaker. Para instalar el paquete *mssql-server-ha*, vea [Instalación de los paquetes de alta disponibilidad y del Agente SQL Server](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages).

Los otros paquetes opcionales para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, la búsqueda de texto completo de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] (*mssql-server-fts*) y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-is*) no se requieren para la alta disponibilidad, ya sea para una FCI o un AG.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Pacemaker para grupos de disponibilidad e instancias de clúster de conmutación por error de AlwaysOn en Linux
Como se indicó anteriormente, el único mecanismo de agrupación en clústeres compatible actualmente con Microsoft en relación con grupos de disponibilidad o instancias de clúster de conmutación por error es Pacemaker con Corosync. Esta sección cubre información básica para comprender la solución, además de cómo planearla e implementarla para configuraciones de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

### <a name="ha-add-onextension-basics"></a>Conceptos básicos de la extensión/complemento de alta disponibilidad
Todas las distribuciones compatibles actualmente incluyen una extensión o complemento de alta disponibilidad, que se basa en la pila de agrupación en clústeres de Pacemaker. Esta pila incorpora dos componentes clave: Pacemaker y Corosync. Todos los componentes de la pila son:
-   Pacemaker: componente principal de la agrupación en clústeres, que hace cosas como coordinar todos los equipos agrupados en clústeres.
-   Corosync: marco de trabajo y conjunto de API que proporcionan aspectos como el cuórum, la capacidad de reiniciar procesos con errores, etc.
-   libQB: se encarga de cuestiones como los registros.
-   Agente de recursos: funcionalidad específica proporcionada para que una aplicación se pueda integrar con Pacemaker.
-   Agente de barrera: scripts/funcionalidad que sirven para aislar nodos y tratarlos en caso de que haya un problema en ellos.
    
> [!NOTE]
> La pila de clúster se conoce comúnmente como Pacemaker en el mundo Linux.

Esta solución es similar en parte (y, al mismo tiempo, diferente en muchas cosas) a implementar configuraciones en clúster mediante Windows. En Windows, la forma de disponibilidad de la agrupación en clústeres, denominada clúster de conmutación por error de Windows Server (WSFC), está integrada en el sistema operativo, y la característica que permite crear un WSFC (clústeres de conmutación por error) está deshabilitada de forma predeterminada. En Windows, los grupos de disponibilidad y las instancias de clúster de conmutación por error se basan en un WSFC y comparten una integración muy estrecha debido al archivo DLL de recurso específico que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] proporciona. Esta solución perfectamente combinada es posible porque todo procede de un mismo proveedor.

![](./media/sql-server-linux-ha-basics/image1.png)

En Linux, aunque todas las distribuciones compatibles tienen Pacemaker disponible, cada una de ellas puede personalizarlo y tener implementaciones y versiones ligeramente diferentes. Algunas de las diferencias se reflejarán en las instrucciones de este artículo. La capa de agrupación en clústeres es de código abierto, por lo que, aunque venga incluida en las distribuciones, no se integra estrechamente de la misma manera a como lo hace un WSFC en Windows. Este es el motivo por el que Microsoft proporciona *mssql-server-ha*, para que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] y la pila de Pacemaker puedan proporcionar una experiencia cercana, si bien no exactamente igual, a los grupos de disponibilidad y las instancias de clúster de conmutación por error en Windows.

Para obtener documentación completa sobre Pacemaker relativa a RHEL y SLES (incluida una explicación más detallada de lo que es cada cosa con información de referencia completa):
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu no tiene una guía sobre disponibilidad.

Para más información sobre la pila completa, vea también la [página de documentación oficial de Pacemaker](https://clusterlabs.org/doc/) en el sitio de Clusterlabs.

### <a name="pacemaker-concepts-and-terminology"></a>Conceptos y terminología de Pacemaker
En esta sección se documentan los conceptos y la terminología comunes de una implementación de Pacemaker.

#### <a name="node"></a>Nodo
Un nodo es un servidor que participa en el clúster. Un clúster de Pacemaker admite de forma nativa hasta 16 nodos. Este número puede ser mayor si Corosync no se está ejecutando en otros nodos, pero Corosync es necesario con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Por lo tanto, el número máximo de nodos que un clúster puede tener en una configuración basada en [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] es 16; este es el límite de Pacemaker, y no tiene nada que ver con los límites máximos impuestos por [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en relación con los grupos de disponibilidad y las instancias de clúster de conmutación por error. 

#### <a name="resource"></a>Resource
Tanto en WSFC como en un clúster de Pacemaker existe el concepto de recurso. Un recurso es una funcionalidad específica que se ejecuta en el contexto del clúster, como un disco o una dirección IP. Por ejemplo, en Pacemaker se pueden crear recursos de grupo de disponibilidad y de instancia de clúster de conmutación por error. Esto no difiere de lo que se lleva a cabo en un WSFC, donde hay un recurso de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] para una instancia de clúster de conmutación por error o para un grupo de disponibilidad al configurar un grupo de disponibilidad, pero no es exactamente lo mismo, dadas las diferencias subyacentes en cuanto a la forma en que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] se integra con Pacemaker.

Pacemaker tiene recursos estándar y de clonación. Los recursos de clonación son aquellos que se ejecutan simultáneamente en todos los nodos. Un ejemplo sería una dirección IP que se ejecuta en varios nodos con fines de equilibrio de carga. Cualquier recurso que se cree para instancias de clúster de conmutación por error usa un recurso estándar, ya que solo un nodo puede hospedar una instancia de clúster de conmutación por error en un momento dado.

Cuando se crea un grupo de disponibilidad, es necesaria una forma especial del recurso de clonación, denominada recurso multiestado. Aunque un grupo de disponibilidad solo tiene una réplica principal, el grupo de disponibilidad en sí se está ejecutando en todos los nodos en los que esté configurada para ejecutarse, y puede permitir potencialmente cosas como el acceso de solo lectura. Dado que se trata de un uso "activo" del nodo, en los recursos existe el concepto de doble estado: maestro y principal/secundario. Para más información, vea [Recursos multiestado: recursos que tienen varios modos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html).

#### <a name="resource-groupssets"></a>Conjuntos/Grupos de recursos
De forma similar a los roles de un WSFC, en un clúster de Pacemaker existe el concepto de un grupo de recursos. Un grupo de recursos (denominado conjunto en SLES) es una colección de recursos que funcionan conjuntamente y que pueden conmutar por error de un nodo a otro como una sola unidad. Los grupos de recursos no pueden contener recursos que estén configurados como principal/secundario; por lo tanto, no se pueden usar con grupos de disponibilidad. Aunque un grupo de recursos se puede usar con instancias de clúster de conmutación por error, esta configuración no suele ser recomendable.

#### <a name="constraints"></a>Restricciones
Los WSFC tienen varios parámetros de recursos, así como dependencias, que indican al WSFC la relación principal/secundario entre dos recursos diferentes. Una dependencia es simplemente una regla que indica al WSFC qué recurso debe estar en línea en primer lugar.

En un clúster de Pacemaker no existe el concepto de dependencias, pero sí hay restricciones. Hay tres tipos de restricción: de colocación, de ubicación y de ordenación.
-   Una restricción de colocación establece si se deben ejecutar (o no) dos recursos en el mismo nodo.
-   Una restricción de ubicación indica al clúster de Pacemaker dónde puede ejecutarse (o no) un recurso.
-   Una restricción de ordenación indica al clúster de Pacemaker el orden en el que deben iniciarse los recursos.

> [!NOTE]
> Las restricciones de colocación no son necesarias en los recursos de un grupo de recursos, ya que todos ellos se consideran una sola unidad.

#### <a name="quorum-fence-agents-and-stonith"></a>Cuórum, agentes de barrera y STONITH
El cuórum en Pacemaker es algo parecido a un WSFC desde un punto de vista conceptual. El propósito general del mecanismo de cuórum de un clúster es asegurarse de que el clúster se mantiene en funcionamiento. Tanto en un WSFC como en los complementos de alta disponibilidad de las distribuciones de Linux existe el concepto de votación, donde cada nodo cuenta para el cuórum. Conviene que haya una mayoría de votos a favor; de lo contrario, en el peor de los casos, el clúster se apagará.

A diferencia de un WSFC, no hay ningún recurso de testigo que funcione con el cuórum. El objetivo es mantener el número de votantes impar, como en el caso de un WSFC. Las consideraciones de configuración de cuórum son diferentes en un grupo de disponibilidad y en una instancia de clúster de conmutación por error.

Los WSFC supervisan el estado de los nodos que participan, y los controlan cuando se produce un problema. Las versiones posteriores de WSFC ofrecen características como poner en cuarentena de un nodo que tiene un comportamiento adecuado o que no está disponible (el nodo no está activo, la comunicación de red está inactiva, etc.). En cuanto a Linux, este tipo de funcionalidad se proporciona mediante un agente de barrera, concepto al que en ocasiones se hace referencia simplemente como "barreras". Sin embargo, estos agentes de barrera suelen ser específicos de la implementación y, a menudo, los facilitan los proveedores de hardware y algunos proveedores de software (como los que suministran hipervisores). Por ejemplo, VMware proporciona un agente de barrera que se puede usar en máquinas virtuales Linux virtualizadas con vSphere.

El cuórum y las barreras entroncan con otro concepto que se conoce como STONITH (acrónimo de "Shoot the Other Node in the Head", que significa "dispara al otro nodo en la cabeza"). STONITH se necesita para tener un clúster de Pacemaker compatible en todas las distribuciones de Linux. Para más información, vea [Barreras en un clúster de alta disponibilidad de Red Hat](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
El archivo `corosync.conf` contiene la configuración del clúster, y se encuentra en `/etc/corosync`. En el transcurso de las operaciones cotidianas normales, este archivo nunca debe editarse si el clúster está configurado correctamente.

#### <a name="cluster-log-location"></a>Ubicación del registro de clúster
Las ubicaciones de registro de los clústeres de Pacemaker difieren en función de la distribución.
-   RHEL y SLES: `/var/log/cluster/corosync.log`
-   Ubuntu: `/var/log/corosync/corosync.log`

Para cambiar la ubicación de registro predeterminada, modifique `corosync.conf`.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Planeación de clústeres de Pacemaker para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
En esta sección se describen los aspectos de planeación importantes relativos a un clúster de Pacemaker.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Virtualización de clústeres de Pacemaker basados en Linux para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
El uso de máquinas virtuales para poner en marcha implementaciones de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] basadas en Linux de grupos de disponibilidad e instancias de clúster de conmutación por error se rige por las mismas reglas que para sus homólogos basados en Windows. Existe un conjunto básico de reglas para la compatibilidad de implementaciones de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] virtualizadas que Microsoft facilita en el [artículo 956893 de la KB de Soporte técnico de Microsoft](https://support.microsoft.com/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment). Cada hipervisor, como Hyper-V de Microsoft o ESXi de VMware, puede tener distintas variaciones aparte de lo anterior, debido a las diferencias en las propias plataformas.

En lo que respecta a los grupos de disponibilidad y las instancias de clúster de conmutación por error virtualizados, asegúrese de que la antiafinidad de los nodos de un clúster de Pacemaker determinado está establecida. Cuando se configuran para alta disponibilidad en una configuración de grupo de disponibilidad o de instancia de clúster de conmutación por error, las máquinas virtuales que hospedan [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] nunca deben ejecutarse en el mismo host de hipervisor. Por ejemplo, si se implementa una instancia de clúster de conmutación por error de dos nodos, debe haber *como mínimo* tres hosts de hipervisor para que haya algún sitio al que las máquinas virtuales que hospedan un nodo puedan ir en caso de que se produzca un error en el host, sobre todo cuando se usan características como Migración en vivo o vMotion.

Para más información, vea:
-   Documentación de Hyper-V: [Uso de la agrupación en clústeres invitados para alta disponibilidad](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   Notas del producto (redactadas para implementaciones basadas en Windows, si bien la mayoría de los conceptos son válidos en este caso también): [Planeación de implementaciones de SQL Server críticas y de alta disponibilidad con VMware vSphere](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

### <a name="networking"></a>Redes
A diferencia de un WSFC, Pacemaker no requiere un nombre dedicado ni una dirección IP dedicada como mínimo para el clúster de Pacemaker en sí. Los grupos de disponibilidad y las instancias de clúster de conmutación por error requerirán direcciones IP (vea la documentación de cada uno para más información), pero no nombres, ya que no hay ningún recurso de nombre de red. SLES permite configurar una dirección IP con fines de administración, pero no es necesario, como se desprende de [Crear el clúster de Pacemaker](sql-server-linux-deploy-pacemaker-cluster.md#create).

Al igual que un WSFC, Pacemaker preferiría redes redundantes, lo que conlleva distintas tarjetas de red (NIC o pNIC, si son físicas) con direcciones IP individuales. Dicho en términos de configuración de clúster, cada dirección IP tendría lo que se conoce como su propio anillo. Sin embargo, igual que ocurre con los WSFC hoy día, muchas implementaciones se virtualizan o se encuentran en la nube pública, donde en realidad solo hay una única NIC virtualizada (vNIC) que se muestra al servidor. Si todas las pNIC y vNIC están conectadas al mismo conmutador físico o virtual, no hay una auténtica redundancia en el nivel de red, por lo que la configuración de varias NIC es un poco un efecto ilusorio para la máquina virtual. La redundancia de red suele estar integrada en el hipervisor en implementaciones virtualizadas, y está integrada en la nube pública.

Una diferencia de tener varias NIC y Pacemaker frente a un WSFC es que Pacemaker permite varias direcciones IP en la misma subred, mientras que un WSFC no. Para más información sobre varias subredes y clústeres de Linux, vea el artículo [Configuración de varias subredes](sql-server-linux-configure-multiple-subnet.md).

### <a name="quorum-and-stonith"></a>Cuórum y STONITH
La configuración y los requisitos de cuórum están relacionados con implementaciones de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] específicas de un grupo de disponibilidad o una instancia de clúster de conmutación por error.

STONITH es necesario en un clúster de Pacemaker compatible. Use la documentación de la distribución para configurar STONITH. Encontrará un ejemplo de SLES en [Barreras basadas en el almacenamiento](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html). También hay un agente STONITH de VMware vCenter para soluciones basadas en ESXI. Para más información, vea [Agente del complemento STONITH para barreras de SOAP de VMware VM vCenter (no oficial)](https://github.com/olafrv/fence_vmware_soap).

### <a name="interoperability"></a>Interoperabilidad
En esta sección se documenta cómo un clúster basado en Linux puede interactuar con un WSFC o con otras distribuciones de Linux.

#### <a name="wsfc"></a>WSFC
Actualmente, no hay ninguna manera directa de que un clúster WSFC y un clúster de Pacemaker funcionen juntos. Esto significa que no existe forma de crear un grupo de disponibilidad o una instancia de clúster de conmutación por error que funcione en un WSFC y en Pacemaker, si bien hay dos soluciones de interoperabilidad diseñadas para grupos de disponibilidad. La única manera de que una instancia de clúster de conmutación por error participe en una configuración multiplataforma es hacerlo como una instancia en uno de estos dos escenarios:
-   Un grupo de disponibilidad que tenga un tipo de clúster None. Para más información, vea la [documentación sobre grupos de disponibilidad](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md) de Windows.
-   Un grupo de disponibilidad distribuido, que es un tipo especial de grupo que permite configurar dos grupos de disponibilidad diferentes como propio grupo de disponibilidad. Para más información sobre los grupos de disponibilidad distribuidos, vea [Grupos de disponibilidad distribuidos](../database-engine/availability-groups/windows/distributed-availability-groups.md).

#### <a name="other-linux-distributions"></a>Otras distribuciones de Linux
En Linux, todos los nodos de un clúster de Pacemaker deben estar en la misma distribución. Esto significa, por ejemplo, que un nodo de RHEL no puede formar parte de un clúster de Pacemaker que tenga un nodo de SLES. La razón principal de esto se ha mencionado antes: cada distribución puede tener versiones y funcionalidades distintas, por lo que las cosas podrían no funcionar correctamente. Si se combinan distribuciones, deberá hacerse igual que al combinar WSFC y Linux: usando clústeres de tipo None o grupos de disponibilidad distribuidos.

## <a name="next-steps"></a>Pasos siguientes
[Implementación de un clúster de Pacemaker para SQL Server en Linux](sql-server-linux-deploy-pacemaker-cluster.md)
