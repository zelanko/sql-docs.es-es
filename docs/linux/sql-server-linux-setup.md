---
title: Guía de instalación de SQL Server 2017 en Linux | Documentos de Microsoft
description: Instalar, actualizar y desinstalar SQL Server en Linux. Este artículo tratan los escenarios en línea, sin conexión y desatendidos.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/06/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: bbf781d365174042f9358fd1e78a26d916f81f99
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323696"
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Guía de instalación para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se proporciona instrucciones para instalar, actualizar y desinstalar SQL Server 2017 en Linux.

> [!TIP]
> Esta guía coves varios escenarios de implementación. Si solo desea obtener instrucciones de instalación paso a paso, vaya a uno de los tutoriales:
> - [Inicio rápido RHEL](quickstart-install-connect-red-hat.md)
> - [Inicio rápido SLES](quickstart-install-connect-suse.md)
> - [Inicio rápido de Ubuntu](quickstart-install-connect-ubuntu.md)
> - [Inicio rápido de docker](quickstart-install-connect-docker.md)

Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](../linux/sql-server-linux-faq.md).

## <a id="supportedplatforms"></a> Plataformas compatibles

SQL Server 2017 es compatible con Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) y Ubuntu. También se admite como una imagen de Docker, que se puede ejecutar en el motor de Docker en Linux o Docker para Windows y Mac.

| Plataforma | Versiones admitidas | Obtener
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 o 7.4 | [Obtener RHEL 7.4](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | SP2 de V12 | [Obtener el Service Pack 2 SLES v12](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Obtener Ubuntu 16.04](http://www.ubuntu.com/download/server)
| **Motor de docker** | 1.8+ | [Obtener Docker](http://www.docker.com/products/overview)

Microsoft también admite la implementación y administración de contenedores de SQL Server mediante OpenShift y Kubernetes.

> [!NOTE]
> SQL Server se prueba y se admite en Linux para las distribuciones enumeradas anteriormente. Si decide instalar SQL Server en un sistema operativo no compatible, revise la **directiva de soporte técnico** sección de la [directiva de soporte técnico de Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) para comprender la compatibilidad con implicaciones.

## <a id="system"></a> Requisitos del sistema

SQL Server 2017 tiene los siguientes requisitos de sistema para Linux:

|||
|-----|-----|
| **Memoria** | 2 GB |
| **Sistema de archivos** | **XFS** o **EXT4** (sí los sistemas de archivos, como **BTRFS**, no son compatibles) |
| **Espacio en disco** | 6 GB |
| **Velocidad del procesador** | 2 GHz |
| **Núcleos de procesador** | 2 núcleos |
| **Tipo de procesador** | solo x64 compatible |

Si usa **Network File System (NFS)** recursos compartidos remotos en producción, tenga en cuenta los siguientes requisitos de soporte técnico:

- Utilice la versión NFS **4.2 o posterior**. Las versiones anteriores de NFS son compatibles con las características necesarias, como fallocate y la creación de archivos dispersos, comunes a sistemas de archivos modernos.
- Busque sólo el **/var/opt/mssql** directorios en el montaje NFS. No se admiten otros archivos, como los archivos binarios del sistema de SQL Server.
- Asegúrese de que los clientes NFS usan la opción 'nolock' al montar el recurso compartido remoto.

## <a id="repositories"></a> Configurar repositorios de origen

Al instalar o actualizar SQL Server, obtendrá la versión más reciente de SQL Server 2017 desde el repositorio de Microsoft configurado. Utilice los tutoriales el **actualización acumulativa (CU)** repositorio. Pero en su lugar, puede configurar la **GDR** repositorio. Para obtener más información sobre los repositorios y cómo configurarlas, consulte [configurar repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

> [!IMPORTANT]
> Si instaló anteriormente un CTP o versión RC de 2017 de SQL Server, debe eliminar el repositorio de vista previa y registrar una disponibilidad General (GA) uno. Para obtener más información, consulte [configurar repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

## <a id="platforms"></a> Instalar SQL Server

Puede instalar a SQL Server en Linux desde la línea de comandos. Para obtener instrucciones, consulte uno de los siguientes tutoriales:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-docker.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

## <a id="upgrade"></a> Actualizar SQL Server

Para actualizar la **mssql server** el paquete a la versión más reciente, use uno de los siguientes comandos en función de la plataforma:

| Plataforma | Comandos de actualización de paquete |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES GRANDE | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

Descargar el paquete más reciente de estos comandos y reemplace los binarios que se encuentran en `/opt/mssql/`. Las bases de datos generado por el usuario y las bases de datos del sistema no se ven afectados por esta operación.

## <a id="rollback"></a> Revertir SQL Server

Para revertir o degradación de SQL Server a una versión anterior, siga estos pasos:

1. Identifique el número de versión para el paquete de SQL Server que desea cambiar a. Para obtener una lista de números de paquete, consulte el [notas de la versión](sql-server-linux-release-notes.md).

1. Degradar a una versión anterior de SQL Server. En los siguientes comandos, reemplace `<version_number>` con el número de versión de SQL Server ha identificado en el paso uno.

   | Plataforma | Comandos de actualización de paquete |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES GRANDE | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> Solo se admite para degradar a una versión dentro de la misma versión principal, como SQL Server 2017.

## <a id="versioncheck"></a> Comprobar la versión instalada de SQL Server

Para comprobar la versión actual y la edición de SQL Server en Linux, utilice el procedimiento siguiente:

1. Si aún no está instalado, instale el [herramientas de línea de comandos de SQL Server](sql-server-linux-setup-tools.md).

1. Use **sqlcmd** para ejecutar un comando de Transact-SQL que muestra la versión de SQL Server y la edición.

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> Desinstalar SQL Server

Para quitar el **mssql server** el paquete en Linux, utilice uno de los siguientes comandos en función de la plataforma:

| Plataforma | Comandos de eliminación de paquetes |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES GRANDE | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

Quitar el paquete no eliminan los archivos de base de datos generada. Si desea eliminar los archivos de base de datos, use el comando siguiente:

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="unattended"></a> Instalación desatendida

Puede realizar una instalación desatendida de la manera siguiente:

- Siga los pasos de la inicial de la [tutoriales](#platforms) para registrar los repositorios e instalar SQL Server.
- Al ejecutar `mssql-conf setup`, establezca [variables de entorno](sql-server-linux-configure-environment-variables.md) y usar el `-n` (sin preguntar) opción.

En el ejemplo siguiente se configura la edición Developer de SQL Server con el **MSSQL_PID** variable de entorno. También acepta los términos de licencia (**ACCEPT_EULA**) y establece la contraseña del usuario administrador (**MSSQL_SA_PASSWORD**). El `-n` parámetro lleva a cabo una instalación sin autorización del usuario donde se extraigan los valores de configuración de las variables de entorno.

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

También puede crear un script que realice otras acciones. Por ejemplo, puede instalar otros paquetes de SQL Server.

Para obtener un script de ejemplo más detallado, vea los ejemplos siguientes:

- [Red Hat script de instalación desatendida](sample-unattended-install-redhat.md)
- [SUSE script de instalación desatendida](sample-unattended-install-suse.md)
- [Ubuntu script de instalación desatendida](sample-unattended-install-ubuntu.md)

## <a id="offline"></a> Instalación sin conexión

Si su equipo Linux no tiene acceso a los repositorios en línea que se utiliza en el [rápidas](#platforms), puede descargar los archivos del paquete directamente. Estos paquetes se encuentran en el repositorio de Microsoft, [ https://packages.microsoft.com ](https://packages.microsoft.com).

> [!TIP]
> Si se ha instalado correctamente con los pasos descritos en las guías de inicio rápidos, no es necesario descargar o instalar manualmente los paquetes de SQL Server. Esta sección es solo para el escenario sin conexión.

1. **Descargue el paquete de motor de base de datos para su plataforma**. Buscar vínculos de descarga de paquete en la sección de detalles del paquete de la [notas de la versión](sql-server-linux-release-notes.md).

1. **Mover el paquete descargado en el equipo Linux**. Si utiliza un equipo diferente para descargar los paquetes, es una manera de mover los paquetes a su equipo Linux con el **scp** comando.

1. **Instalar el paquete del motor de base de datos**. Utilice uno de los siguientes comandos en función de la plataforma. Reemplace el nombre de archivo de paquete en este ejemplo con el nombre exacto que se descargó.

   | Plataforma | Comando de instalación de paquete |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES GRANDE | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > También puede instalar los paquetes RPM (RHEL y SLES) con el `rpm -ivh` comando, pero los comandos en la tabla anterior instalan automáticamente las dependencias si aprueba disponible en repositorios.

1. **Resolver las dependencias que faltan**: es posible que tenga dependencias que faltan en este momento. De lo contrario, puede omitir este paso. En Ubuntu, si se tiene acceso a repositorios aprobados que contiene esas dependencias, la solución más fácil es utilizar el `apt-get -f install` comando. Este comando también completa la instalación de SQL Server. Para inspeccionar manualmente las dependencias, use los siguientes comandos:

   | Plataforma | Mostrar dependencias (comando) |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES GRANDE | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   Después de resolver las dependencias que faltan, intente instalar de nuevo el paquete de server mssql.

1. **Completar la instalación de SQL Server**. Use **mssql-conf** para completar la instalación de SQL Server:

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="optional-sql-server-features"></a>Características opcionales de SQL Server

Después de la instalación, también puede instalar o habilitar características opcionales de SQL Server.

- [Herramientas de línea de comandos de SQL Server](sql-server-linux-setup-tools.md)
- [Agente SQL Server](sql-server-linux-setup-sql-agent.md)
- [Búsqueda de texto completo de SQL Server](sql-server-linux-setup-full-text-search.md)
- [Servicios de integración de SQL Server (Ubuntu)](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](sql-server-linux-faq.md).
