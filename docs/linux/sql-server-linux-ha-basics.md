---
title: Aspectos básicos de la disponibilidad de SQL Server para las implementaciones de Linux | Microsoft Docs
description: ''
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: b33acbcf74857cd6a2def74f3596e3dda2a034a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720873"
---
# <a name="sql-server-availability-basics-for-linux-deployments"></a>Aspectos básicos de la disponibilidad de SQL Server para las implementaciones de Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

A partir de [!INCLUDE[sssql17-md](../includes/sssql17-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] es compatible con Linux y Windows. Basado en Windows, como [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] las implementaciones, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] bases de datos y las instancias deben ser altamente disponible en Linux. En este artículo se trata los aspectos técnicos de planeación e implementación de alta disponibilidad basado en Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] bases de datos y las instancias, así como algunas de las diferencias de las instalaciones basadas en Windows. Dado que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pueden ser nuevos para los profesionales de TI de Linux y Linux pueden ser nuevos para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] los profesionales de TI, el artículo a veces presenta conceptos que pueden ser familiares para algunos y familiar para otros usuarios.

## <a name="includessnoversion-mdincludesssnoversion-mdmd-availability-options-for-linux-deployments"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Opciones de disponibilidad para las implementaciones de Linux
Además de la copia de seguridad y restauración, las mismas tres características de disponibilidad están disponibles en Linux en cuanto a las implementaciones basadas en Windows:
-   Grupos de disponibilidad (AG) AlwaysOn
-   Instancias de clúster de conmutación por error (FCI) AlwaysOn
-   [Trasvase de registros](sql-server-linux-use-log-shipping.md)

En Windows, las fci siempre requieren un clúster de conmutación por error de Windows Server (WSFC) subyacente. Según el escenario de implementación, un grupo de disponibilidad normalmente requiere un clúster de WSFC subyacente, con la excepción que se va a la nueva variante en None [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]. No existe un WSFC en Linux. Los clústeres de implementación en Linux se describen en la sección [instancias de Pacemaker para clúster de conmutación por error y grupos de disponibilidad AlwaysOn en Linux](#pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux).

## <a name="a-quick-linux-primer"></a>Ver una rápida introducción de Linux
Si bien algunas instalaciones de Linux se pueden instalar con una interfaz, la mayoría son no, lo que significa que casi todo en el nivel de sistema operativo se realiza a través de la línea de comandos. El término común para esta línea de comandos en el mundo de Linux es un *shell de bash*.

En Linux, muchos comandos deben ejecutarse con privilegios elevados, al igual que muchas cosas tienen que realizarse en Windows Server como administrador. Hay dos métodos principales para ejecutar con privilegios elevados:
1. Ejecutar en el contexto del usuario adecuado. Para cambiar a otro usuario, use el comando `su`. Si `su` se ejecuta en su propio sin un nombre de usuario, siempre que sepa la contraseña, ahora estará en un shell como *raíz*.
   
2. La más común y seguridad consciente para ejecutar las cosas consiste en usar `sudo` antes de ejecutar cualquier cosa. Muchos de los ejemplos de este artículo utilizan `sudo`.

Algunos comandos habituales, cada uno de los cuales tienen diversos modificadores y opciones que pueden ser investigadas en línea:
-   `cd` : cambiar el directorio
-   `chmod` : cambiar los permisos de un archivo o directorio
-   `chown` : cambiar la propiedad de un archivo o directorio
-   `ls` : mostrar el contenido de un directorio
-   `mkdir` : cree una carpeta (directorio) en una unidad
-   `mv` : mover un archivo desde una ubicación a otra
-   `ps` : mostrar todos los procesos de trabajo
-   `rm` : elimina un archivo localmente en un servidor
-   `rmdir` : eliminar una carpeta (directorio)
-   `systemctl` : iniciar, detener o habilitar los servicios
-   Comandos del editor de texto. En Linux, hay varias opciones del editor de texto, como vi, emacs.

## <a name="common-tasks-for-availability-configurations-of-includessnoversion-mdincludesssnoversion-mdmd-on-linux"></a>Tareas comunes para las configuraciones de disponibilidad de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux
Esta sección tratan las tareas que son comunes a todos los basados en Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implementaciones.

### <a name="ensure-that-files-can-be-copied"></a>Asegúrese de que se pueden copiar archivos
Copiar archivos desde un servidor a otro es una tarea que cualquier usuario con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, debe ser capaz de hacer. Esta tarea es muy importante para las configuraciones de grupo de disponibilidad.

Cosas como problemas de permisos pueden existir en Linux, así como en las instalaciones basadas en Windows. Sin embargo, aquellos que estén familiarizados con la copia del servidor en Windows pueden no estar familiarizados con cómo se hace en Linux. Un método común consiste en usar la utilidad de línea de comandos `scp`, que es el acrónimo de copia de seguridad. En segundo plano, `scp` usa OpenSSH. SSH es el acrónimo de shell seguro. Dependiendo de la distribución de Linux, no se puede instalar OpenSSH propio. Si no es así, OpenSSH debe instalarse primero. Para obtener más información sobre cómo configurar OpenSSH, consulte la información en los siguientes vínculos para cada distribución:
-   [Red Hat Enterprise Linux (RHEL)](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-OpenSSH.html)
-   [SUSE Linux Enterprise Server (SLES)](https://en.opensuse.org/SDB:Configure_openSSH)
-   [Ubuntu](https://help.ubuntu.com/community/SSH/OpenSSH/Configuring)

Cuando se usa `scp`, debe proporcionar las credenciales del servidor si no es el origen o destino. Por ejemplo, si se usa

```bash
scp MyAGCert.cer username@servername:/folder/subfolder
```

copia el archivo MyAGCert.cer en la carpeta especificada en el otro servidor. Tenga en cuenta que debe tener permisos: y, posiblemente, la propiedad – del archivo para copiarlo, por lo que `chown` también es posible que deba emplearse antes de copiar. De forma similar, en el lado receptor, el usuario correcto necesita acceso para manipular el archivo. Por ejemplo, para restaurar ese archivo de certificado, el `mssql` usuario debe poder tener acceso a ella.

Samba, que es la variante de Linux del bloque de mensajes del servidor (SMB), también puede utilizarse para crear recursos compartidos de acceso a las rutas de acceso UNC, como `\\SERVERNAME\SHARE`. Para obtener más información sobre la configuración de Samba, consulte la información en los siguientes vínculos para cada distribución:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Managing_Confined_Services/chap-Managing_Confined_Services-Samba.html)
-   [SLES](https://www.suse.com/documentation/sles11/book_sle_admin/data/cha_samba.html)
-   [Ubuntu](https://help.ubuntu.com/community/Samba)

También se pueden usar recursos compartidos de SMB basado en Windows; No es necesario estar basado en Linux, siempre que la parte cliente de Samba está configurada correctamente en el servidor Linux que hospeda recursos compartidos de SMB [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] y el recurso compartido tiene el derecho de acceso. Para los miembros de un entorno mixto, esto sería una manera de aprovechar la infraestructura existente para basado en Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implementaciones.

Algo que es importante es que la versión de Samba implementado debe ser compatible de SMB 3.0. Cuando se agregó compatibilidad con SMB en [!INCLUDE[sssql11-md](../includes/sssql11-md.md)], es necesario que todos los recursos compartidos para admitir SMB 3.0. Si usas Samba para el recurso compartido y no a Windows Server, debe usar el recurso compartido de Samba Samba 4.0 o posterior y lo ideal es que 4.3 o posterior, que es compatible con SMB 3.1.1. Es una buena fuente de información sobre SMB y Linux [SMB3 en Samba](http://events.linuxfoundation.org/sites/events/files/slides/smb3-in-samba.pr__0.pdf).

Por último, el uso de un recurso compartido de red archivos system (NFS) es una opción. Uso de NFS no es una opción en implementaciones basadas en Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]y solo se puede usar para las implementaciones basadas en Linux.

### <a name="configure-the-firewall"></a>Configuración del firewall
Al igual que Windows, las distribuciones de Linux tienen un firewall integrado. Si su empresa usa un firewall externo a los servidores, la deshabilitación de los firewalls en Linux puede ser aceptable. Sin embargo, independientemente de que el firewall está habilitado, los puertos deben abrirse. En la tabla siguiente se documenta los puertos comunes necesarios para alta disponibilidad [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implementaciones en Linux.

| Número de puerto | Tipo     | Descripción                                                                                                                 |
|-------------|----------|-----------------------------------------------------------------------------------------------------------------------------|
| 111         | TCP/UDP  | NFS: `rpcbind/sunrpc`                                                                                                    |
| 135         | TCP      | Samba (si se usa): asignador de puntos finales                                                                                          |
| 137         | UDP      | Samba (si se usa): servicio de nombres NetBIOS                                                                                      |
| 138         | UDP      | Samba (si se usa): datagrama NetBIOS                                                                                          |
| 139         | TCP      | Samba (si se usa): sesión NetBIOS                                                                                           |
| 445         | TCP      | Samba (si se usa): SMB a través de TCP                                                                                              |
| 1433        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] –; el puerto predeterminado Si lo desea, puede cambiar con `mssql-conf set network.tcpport <portnumber>`                       |
| 2049        | TCP, UDP | NFS (si se usa)                                                                                                               |
| 2224        | TCP      | Pacemaker: usando `pcsd`                                                                                                |
| 3121        | TCP      | Pacemaker: necesario si hay nodos remotos de Pacemaker                                                                    |
| 3260        | TCP      | iSCSI Initiator (si se usa): se puede modificar en `/etc/iscsi/iscsid.config` (RHEL), pero debe coincidir con el puerto de destino iSCSI |
| 5022        | TCP      | [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] -usa para un punto de conexión del grupo de disponibilidad; el puerto predeterminado se puede cambiar al crear el punto de conexión                                |
| 5403        | TCP      | Pacemaker                                                                                                                   |
| 5404        | UDP      | Pacemaker: requerido Corosync si mediante multidifusión UDP                                                                     |
| 5405        | UDP      | Pacemaker: requerido por Corosync                                                                                            |
| 21064       | TCP      | Pacemaker: requerido por los recursos mediante DLM                                                                                 |
| Variable    | TCP      | Puerto de punto de conexión del grupo de disponibilidad; el valor predeterminado es 5022                                                                                           |
| Variable    | TCP      | El puerto para NFS: `LOCKD_TCPPORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL)                                              |
| Variable    | UDP      | El puerto para NFS: `LOCKD_UDPPORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL)                                              |
| Variable    | TCP/UDP  | El puerto para NFS: `MOUNTD_PORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL)                                                |
| Variable    | TCP/UDP  | El puerto para NFS: `STATD_PORT` (se encuentra en `/etc/sysconfig/nfs` en RHEL)                                                 |

Para obtener información sobre los puertos adicionales que pueden usarse en Samba, consulte [uso del puerto Samba](https://wiki.samba.org/index.php/Samba_Port_Usage).

Por el contrario, el nombre del servicio en la sección Linux también puede agregarse como una excepción en lugar del puerto; Por ejemplo, `high-availability` para Pacemaker. Hacer referencia a la distribución de los nombres si esta es la dirección que desea llevar a cabo. Por ejemplo, en RHEL es el comando para agregar en Pacemaker

```bash
sudo firewall-cmd --permanent --add-service=high-availability
```

**Documentación del firewall:**
-   [RHEL](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/high_availability_add-on_reference/s1-firewalls-haar)
-   [SLES](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html)

### <a name="install-includessnoversion-mdincludesssnoversion-mdmd-packages-for-availability"></a>Instalar [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] paquetes para disponibilidad
En basado en Windows [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instalación, algunos componentes se instalan incluso en una instalación básica del motor, mientras que otros no. En Linux, solo el [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] motor se instala como parte del proceso de instalación. Todo lo demás es opcional. Para alta disponibilidad [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] instancias en Linux, se deben instalar dos paquetes con [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]: [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente (*mssql-server-agent*) y el paquete de alta disponibilidad (HA) ( *MSSQL-server-ha*). Mientras [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente es técnicamente opcional, es [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]del programador de trabajos y es obligatorio para trasvase de registros, por lo que se recomienda la instalación. En las instalaciones basadas en Windows, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente no es opcional.

>[!NOTE]
>Para aquellos que desconozcan [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente es [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]del programador de trabajos integrado. Es una forma común de los DBA programar cosas como copias de seguridad y otras [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] mantenimiento. A diferencia de una instalación basada en Windows de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] donde [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente es un servicio completamente diferente, en Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente se ejecuta en el contexto de [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] propio.

Cuando se configuran grupos de disponibilidad o fci en una configuración basada en Windows, son compatibles con clústeres. Compatibilidad con clústeres significa que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] tiene archivos DLL que conoce (sqagtres.dll y sqsrvres.dll para fci, hadrres.dll para AG) un WSFC de recurso específico y el WSFC sirven para asegurarse de que el [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] funcionalidad en clúster está activo, ejecutando, y funciona correctamente. Porque la agrupación en clústeres es externo no solo a [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] pero Linux Sí, Microsoft tenía código el equivalente de una DLL de recursos para las implementaciones de grupo de disponibilidad basado en Linux y FCI. Se trata de la *mssql-server-ha* del paquete, también conocido como el [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] agente de recursos para Pacemaker. Para instalar el *mssql-server-ha* de paquetes, vea [instalar los paquetes de alta disponibilidad y el Agente SQL Server](sql-server-linux-deploy-pacemaker-cluster.md#install-the-sql-server-ha-and-sql-server-agent-packages).

Los otros paquetes opcionales para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] en Linux, [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Full-Text Search (*mssql-server-fts*) y [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Integration Services (*mssql-server-es*), no son se requiere para alta disponibilidad, ya sea por una FCI o un grupo de disponibilidad.

## <a name="pacemaker-for-always-on-availability-groups-and-failover-cluster-instances-on-linux"></a>Pacemaker para grupos de disponibilidad AlwaysOn y las instancias de clúster de conmutación por error en Linux
Anterior como se indicó, el único mecanismo de agrupación en clústeres admitido actualmente por Microsoft para grupos de disponibilidad y fci es Pacemaker con Corosync. Esta sección tratan la información básica para comprender la solución, así como cómo planear e implementar para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] configuraciones.

### <a name="ha-add-onextension-basics"></a>Conceptos básicos del complemento prácticos/extensión de alta disponibilidad
Todas las distribuciones compatibles actualmente incluyen un complemento-prácticos/extensión de alta disponibilidad, que se basa en la pila de clústeres de Pacemaker. Esta pila incorpora dos componentes clave: Pacemaker y Corosync. Todos los componentes de la pila son:
-   Pacemaker: el núcleo de agrupación en clústeres de componente, que permite hacer cosas como coordenada entre las máquinas clúster.
-   Corosync: un marco y conjunto de API que proporciona cosas como el quórum, la capacidad de los procesos no se puede reiniciar y así sucesivamente.
-   libQB – proporciona cosas como el registro.
-   Agente de recursos: funcionalidad específica que proporciona para que una aplicación puede integrar con Pacemaker.
-   Valla de secuencias de comandos o funcionalidad que ayudarte a aislar los nodos y resolverlos si tienen problemas del agente.
    
> [!NOTE]
> La pila de clúster se conoce normalmente como Pacemaker en el mundo de Linux.

Esta solución es en cierto modo similar a, pero en muchos aspectos diferentes de la implementación de las configuraciones en clúster con Windows. En Windows, el formulario de la disponibilidad de agrupación en clústeres, llama a un clúster de conmutación por error de Windows Server (WSFC), está integrado en el sistema operativo y la característica que permite la creación de un clúster de WSFC, agrupación en clústeres de conmutación por error, se deshabilita de forma predeterminada. En Windows, grupos de disponibilidad fci se basan en un WSFC y comparten una estrecha integración debido a la DLL que proporciona de recursos específico [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Esta solución estrechamente acoplada en general es posible porque está todo desde un proveedor.

![](./media/sql-server-linux-ha-basics/image1.png)

En Linux, mientras que cada distribución compatible tiene Pacemaker disponible, cada distribución puede personalizar y tienen versiones e implementaciones ligeramente diferentes. Algunas de las diferencias se reflejarán en las instrucciones de este artículo. El nivel de agrupación en clústeres es código abierto, por lo que, aunque distribuye con las distribuciones, no está estrechamente integrado en la misma forma un clúster WSFC en Windows. Es por esta razón que proporciona Microsoft *mssql-server-ha*, de modo que [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] y la pila de Pacemaker puede proporcionar cerca, pero no exactamente la misma experiencia para los grupos de disponibilidad y fci en Windows.

Para obtener documentación completa en Pacemaker, que incluye una explicación más detallada de lo que todo lo que es con información de referencia completa, para RHEL y SLES:
-   [RHEL](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/High_Availability_Add-On_Reference/ch-overview-HAAR.html)
-   [SLES](https://www.suse.com/documentation/sle_ha/book_sleha/data/book_sleha.html)

Ubuntu no tiene una guía para la disponibilidad.

Para obtener más información acerca de la pila completa, consulte también el sitio oficial [página de documentación de Pacemaker](http://clusterlabs.org/doc/) en el sitio Clusterlabs.

### <a name="pacemaker-concepts-and-terminology"></a>Terminología y conceptos de pacemaker
Esta sección describe los conceptos y terminología para una implementación de Pacemaker comunes.

#### <a name="node"></a>Nodo
Un nodo es un servidor que participan en el clúster. Un clúster de Pacemaker admite hasta 16 nodos de forma nativa. Este número se puede superar si Corosync no se está ejecutando en los nodos adicionales, pero es necesario para Corosync [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. Por lo tanto, el número máximo de nodos de un clúster puede tener para cualquier [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-en función de configuración es 16; esto es el límite de Pacemaker y no tiene nada que ver con las limitaciones máximas para grupos de disponibilidad o fci impuestas por [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]. 

#### <a name="resource"></a>Recurso
Un clúster WSFC y un clúster de Pacemaker tienen el concepto de un recurso. Un recurso es una funcionalidad específica que se ejecuta en el contexto del clúster, como un disco o una dirección IP. Por ejemplo, en Pacemaker pueden crear los recursos de FCI y grupo de disponibilidad. Esto no es muy distinta a lo que se realiza en un WSFC, donde verá un [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] recurso para ser una FCI o un grupo de disponibilidad al configurar un grupo de disponibilidad, pero es no es exactamente el mismo debido a las diferencias en cómo subyacentes [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] se integra con Pacemaker.

Pacemaker tiene recursos estándar y el clon. Clone los recursos son las que se ejecutan simultáneamente en todos los nodos. Un ejemplo sería una dirección IP que se ejecuta en varios nodos para equilibrar la carga. Cualquier recurso que se crea para fci usa un recurso estándar, ya que sólo un nodo puede hospedar una FCI en un momento dado.

Cuando se crea un grupo de disponibilidad, requiere una forma especializada de un recurso de clon llama a un recurso de varios estado. Aunque un grupo de disponibilidad solo tiene una réplica principal, el grupo de disponibilidad se está ejecutando en todos los nodos que está configurado para funcionar en y puede permitir que las cosas, como el acceso de solo lectura. Se trata de un uso "activo" del nodo, los recursos tienen el concepto de dos estados: principal y secundario. Para obtener más información, consulte [varios Estados recursos: recursos que tienen varios modos](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/s1-multistateresource-HAAR.html).

#### <a name="resource-groupssets"></a>Grupos o conjuntos de recursos
Un clúster de Pacemaker similares a los roles en un WSFC, tiene el concepto de un grupo de recursos. Un grupo de recursos (llamado un conjunto en SLES) es una colección de recursos que funcionan juntos y puede conmutar por error de un nodo a otro como una sola unidad. Grupos de recursos no pueden contener recursos que están configurados como maestro/subordinado; por lo tanto, no se puede usar para grupos de disponibilidad. Aunque un grupo de recursos se puede usar para fci, no es generalmente una configuración recomendada.

#### <a name="constraints"></a>Restricciones
Wsfc tiene varios parámetros para los recursos, así como aspectos como las dependencias, que indican el WSFC de una relación primario-secundario entre dos recursos distintos. Una dependencia es simplemente una regla que indica que el WSFC qué recursos deban estar en línea en primer lugar.

Un clúster de Pacemaker no tiene el concepto de dependencias, pero existen restricciones. Hay tres tipos de restricciones: ubicación compartida, la ubicación y la ordenación.
-   Una restricción de colocación se aplica si se deben ejecutar dos recursos en el mismo nodo.
-   Una restricción de ubicación indica al clúster de Pacemaker en un recurso puede (o no) ejecutar.
-   Una restricción de ordenación indica el clúster de Pacemaker en el orden en el que se deben iniciar los recursos.

> [!NOTE]
> Restricciones de colocación no son necesarias para los recursos de un grupo de recursos, puesto que todos los que se ven como una sola unidad.

#### <a name="quorum-fence-agents-and-stonith"></a>Quórum, los agentes de la barrera y STONITH
Es algo similar a un clúster de WSFC en el concepto de quórum en Pacemaker. El propósito del mecanismo de quórum de un clúster de todo es asegurarse de que el clúster permanece en marcha. Un clúster WSFC y los complementos de alta disponibilidad para las distribuciones de Linux tienen el concepto de votación, donde cada nodo cuenta hacia el cuórum. Desea que la mayoría de los votos, de lo contrario, en un escenario del peor caso, se cerrará el clúster.

A diferencia de un clúster de WSFC, no hay ningún recurso de testigo para trabajar con quórum. Al igual que un clúster de WSFC, el objetivo es mantener el número de los votantes impares. Configuración de quórum tiene diferentes consideraciones para grupos de disponibilidad de las fci.

Wsfc supervisar el estado de los nodos que participan y controlarlos cuando se produce un problema. Las versiones posteriores de Wsfc ofrecen características tales como poner en cuarentena un nodo que es el comportamiento incorrecto o no está disponible (nodo no está activado, la comunicación de red es hacia abajo, etcetera.). En el lado de Linux, este tipo de funcionalidad se proporciona un agente de barrera. El concepto se conoce a veces como barrera. Sin embargo, estos agentes de barrera son generalmente específicos de la implementación y, a menudo proporcionan por los proveedores de hardware y algunos proveedores de software, como aquellos que proporcionan los hipervisores. Por ejemplo, VMware proporciona a un agente de barrera que puede usarse para máquinas virtuales de Linux virtualizadas con vSphere.

Quórum y vallado valores equivalentes en otro concepto llamado STONITH o Shoot the Other Node en el encabezado. STONITH se debe tener un clúster de Pacemaker compatibles en todas las distribuciones de Linux. Para obtener más información, consulte [barrera en un clúster de disponibilidad alta de Red Hat](https://access.redhat.com/solutions/15575) (RHEL).

#### <a name="corosyncconf"></a>corosync.conf
El `corosync.conf` archivo contiene la configuración del clúster. Se encuentra en `/etc/corosync`. En el transcurso de las operaciones diarias normales, este archivo debería tener que modificarse si el clúster se ha configurado correctamente.

#### <a name="cluster-log-location"></a>Ubicación del registro de clúster
Ubicaciones del registro para los clústeres de Pacemaker varían según la distribución.
-   RHEL y SLES: `/var/log/cluster/corosync.log`
-   Ubuntu: `/var/log/corosync/corosync.log`

Para cambiar la ubicación del registro de forma predeterminada, modifique `corosync.conf`.

## <a name="plan-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Planeamiento de clústeres de Pacemaker para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
En esta sección se describe los puntos de planeación importantes para un clúster de Pacemaker.

### <a name="virtualizing-linux-based-pacemaker-clusters-for-includessnoversion-mdincludesssnoversion-mdmd"></a>Los clústeres de virtualización de Pacemaker en Linux para [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
Uso de máquinas virtuales para implementar basado en Linux [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] las implementaciones de grupos de disponibilidad y fci está cubierto por las mismas reglas que sus equivalentes basados en Windows. Hay un conjunto básico de reglas para la compatibilidad de virtualizado [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] implementaciones proporcionadas por Microsoft en [956893 de KB del soporte técnico de Microsoft](https://support.microsoft.com/en-us/help/956893/support-policy-for-microsoft-sql-server-products-that-are-running-in-a-hardware-virtualization-environment). Los hipervisores diferentes, como Microsoft Hyper-V y VMware ESXi pueden tienen varianzas diferentes sobre eso, debido a diferencias en las plataformas a sí mismos.

Cuando se trata de grupos de disponibilidad y fci bajo virtualización, asegúrese de que antiafinidad se establece para los nodos de un clúster de Pacemaker determinado. Cuando se configura para alta disponibilidad en una configuración de grupo de disponibilidad o FCI, las máquinas virtuales que hospedan [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] nunca debe ejecutarse en el mismo host del hipervisor. Por ejemplo, si se implementa una FCI de dos nodos, debería ser *al menos* tres hosts de hipervisor en el modo que haya en algún lugar de una de las máquinas virtuales de un nodo de hospedaje para ir si se produce un error de host, especialmente si usa características como Live Migración o vMotion.

Para obtener más detalles, consulte:
-   Documentación de Hyper-V – [usar clústeres invitados para alta disponibilidad](https://technet.microsoft.com/library/dn440540(v=ws.11).aspx)
-   Notas del producto (escrito para las implementaciones basadas en Windows, pero la mayoría de los conceptos que todavía se aplican –) [planear alta disponibilidad, SQL Server implementaciones críticas con VMware vSphere](http://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/solutions/vmware-vsphere-highly-available-mission-critical-sql-server-deployments.pdf)

>[!NOTE]
>RHEL con un clúster de Pacemaker con STONITH no es compatible aún con Hyper-V. Hasta que se admite para obtener más información y actualizaciones, consulte [directivas de soporte técnico para los clústeres de alta disponibilidad RHEL](https://access.redhat.com/articles/29440#3physical_host_mixing).

### <a name="networking"></a>Redes
A diferencia de un clúster de WSFC, Pacemaker no requiere un nombre dedicado o al menos una dirección IP dedicada para el propio clúster de Pacemaker. Grupos de disponibilidad y fci requerirá las direcciones IP (consulte la documentación de cada uno de ellos para obtener más información), pero no los nombres, ya que no hay ningún recurso de nombre de red. SLES permite que la configuración de una dirección IP para fines de administración, pero no es necesario, como puede verse en [crear el clúster de Pacemaker](sql-server-linux-deploy-pacemaker-cluster.md#create).

Al igual que un clúster de WSFC, Pacemaker sería preferible redes redundantes, lo que significa que las tarjetas de red distinto (NIC o pNICs para física) tener direcciones IP individuales. En cuanto a la configuración del clúster, cada dirección IP tendría lo que se conoce como su propio anillo. Sin embargo, tal como con Wsfc hoy en día, se virtualizan muchas implementaciones o en la nube pública donde realmente no hay una sola virtualizados NIC (vNIC) presentado al servidor. Si todos los pNICs y VNIC está conectado al mismo conmutador físico o virtual, no hay ninguna redundancia true en el nivel de red, por lo que la configuración de varias NIC es un poco de una ilusión a la máquina virtual. Redundancia de red normalmente se compila en el hipervisor para implementaciones virtualizadas y definitivamente está integrada en la nube pública.

Una diferencia con varias NIC y Pacemaker frente a un clúster WSFC es que Pacemaker permite varias direcciones IP en la misma subred, mientras que un clúster WSFC no. Para obtener más información en varias subredes y los clústeres de Linux, consulte el artículo [configurar varias subredes](sql-server-linux-configure-multiple-subnet.md).

### <a name="quorum-and-stonith"></a>Quórum y STONITH
Configuración de quórum y requisitos están relacionados con implementaciones de grupo de disponibilidad o específicas de FCI [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)].

STONITH se requiere para un clúster de Pacemaker compatibles. Use la documentación de la distribución para configurar STONITH. Un ejemplo es en [vallado basado en almacenamiento](https://www.suse.com/documentation/sle_ha/book_sleha/data/sec_ha_storage_protect_fencing.html) para SLES. También hay un agente STONITH para vCenter de VMware para las soluciones basadas en ESXI. Para obtener más información, consulte [Stonith complemento de agente de barrera de VMWare VM VCenter SOAP (Unofficial)](https://github.com/olafrv/fence_vmware_soap).

> [!NOTE]
> Al redactar este artículo, Hyper-V no tiene una solución de STONITH. Esto es cierto para implementaciones locales y también afecta a las implementaciones de Pacemaker basada en Azure con ciertas distribuciones, como RHEL.

### <a name="interoperability"></a>Interoperabilidad
Esta sección describe cómo un clúster basado en Linux puede interactuar con un clúster WSFC o con otras distribuciones de Linux.

#### <a name="wsfc"></a>WSFC
Actualmente, no hay ninguna manera directa de un clúster de WSFC y un clúster de Pacemaker para que trabajen juntos. Esto significa que no hay ninguna manera de crear un grupo de disponibilidad o FCI que funciona a través de un clúster WSFC y Pacemaker. Sin embargo, hay dos soluciones de interoperabilidad, ambos de los cuales están diseñados para grupos de disponibilidad. La única forma de que una FCI puede participar en una configuración de desarrollo multiplataforma es si participa como una instancia de uno de estos dos escenarios:
-   Un grupo de disponibilidad con un tipo de clúster ninguno. Para obtener más información, consulte el Windows [documentación de grupos de disponibilidad](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md).
-   Un grupo de disponibilidad distribuido, que es un tipo especial de grupo de disponibilidad que permite que dos grupos de disponibilidad diferentes se configure como su propio grupo de disponibilidad. Para obtener más información sobre grupos de disponibilidad distribuidos, consulte la documentación [grupos de disponibilidad distribuidos](../database-engine/availability-groups/windows/distributed-availability-groups.md).

#### <a name="other-linux-distributions"></a>Otras distribuciones de Linux
En Linux, todos los nodos de un clúster de Pacemaker deben estar en la misma distribución. Por ejemplo, esto significa que un nodo RHEL no puede formar parte de un clúster de Pacemaker que tiene un nodo SLES. La razón principal para que esto ha mencionado anteriormente: las distribuciones pueden tener diferentes versiones y funcionalidad, por lo que podría no funcionará correctamente. Mezclar las distribuciones tiene el mismo artículo que mezclar Wsfc y Linux: use la opción Ninguno o distributed AG.

## <a name="next-steps"></a>Pasos siguientes
[Implementar un clúster marcapasos para SQL Server en Linux](sql-server-linux-deploy-pacemaker-cluster.md)
