---
title: Guía de instalación para SQL Server en Linux
titleSuffix: SQL Server
description: Instalar, actualizar y desinstalar SQL Server en Linux. Este artículo tratan los escenarios en línea, sin conexión y desatendidos.
author: VanMSFT
ms.author: vanto
ms.date: 05/28/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sqlfreshmay19
ms.technology: linux
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.openlocfilehash: 7f4b2aa37b20cceaa3269527c95bfa97a2daa311
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032436"
---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Guía de instalación para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este artículo proporcionan instrucciones para instalar, actualizar y desinstalar SQL Server 2017 y la vista previa de 2019 de SQL Server en Linux.

> [!TIP]
> Esta guía coves varios escenarios de implementación. Si solo desea para obtener instrucciones de instalación paso a paso, vaya a uno de los inicios rápidos:
> - [Guía de inicio rápido RHEL](quickstart-install-connect-red-hat.md)
> - [Guía de inicio rápido SLES](quickstart-install-connect-suse.md)
> - [Inicio rápido de Ubuntu](quickstart-install-connect-ubuntu.md)
> - [Guía de inicio rápido de docker](quickstart-install-connect-docker.md)

Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](../linux/sql-server-linux-faq.md).

## <a id="supportedplatforms"></a> Plataformas compatibles

SQL Server 2017 es compatible con Ubuntu, SUSE Linux Enterprise Server (SLES) y Red Hat Enterprise Linux (RHEL). También se admite como una imagen de Docker, que puede ejecutar en el motor de Docker en Linux o Docker para Windows o Mac.

| Plataforma | Versiones admitidas | Obtener
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3, 7.4, 7.5, 7.6 | [Obtener RHEL 7.6](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | v12 SP2 | [Obtener el Service Pack 2 SLES v12](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Obtener Ubuntu 16.04](http://releases.ubuntu.com/xenial/)
| **Motor de docker** | 1.8+ | [Obtener Docker](https://www.docker.com/get-started)

Microsoft también admite la implementación y administración de contenedores de SQL Server mediante el uso de OpenShift y Kubernetes.

> [!NOTE]
> SQL Server se ha probado y compatible con Linux para las distribuciones enumeradas anteriormente. Si decide instalar SQL Server en un sistema operativo no compatible, revise el **directiva de soporte técnico** sección de la [directiva de soporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) para entender la compatibilidad implicaciones.

## <a id="system"></a> Requisitos del sistema

SQL Server 2017 tiene los siguientes requisitos del sistema para Linux:

|||
|-----|-----|
| **Memoria** | 2 GB |
| **Sistema de archivos** | **XFS** o **EXT4** (otros sistemas de archivos como **BTRFS**, no son compatibles) |
| **Espacio en disco** | 6 GB |
| **Velocidad del procesador** | 2 GHz |
| **Núcleos de procesador** | 2 núcleos |
| **Tipo de procesador** | compatible con x64 64 solo |

Si usas **Network File System (NFS)** recursos compartidos remotos en producción, tenga en cuenta los siguientes requisitos de soporte técnico:

- Use la versión NFS **4.2 o superior**. Las versiones anteriores de NFS no admiten las características necesarias, como fallocate y creación del archivo disperso, comunes a los modernos sistemas de archivos.
- Busque sólo el **/var/opt/mssql** directorios en el montaje NFS. Otros archivos, como los archivos binarios del sistema de SQL Server, no se admiten.
- Asegúrese de que los clientes NFS usan la opción "nolock" al montar el recurso compartido remoto.

## <a id="repositories"></a> Configurar repositorios de código fuente

Al instalar o actualizar SQL Server, obtenga la versión más reciente de SQL Server desde el repositorio de Microsoft configurado. Los tutoriales rápidos de usar la actualización acumulativa de SQL Server 2017 **CU** repositorio. Pero en su lugar, puede configurar el **GDR** repositorio o el **Preview (vNext)** repositorio. Para obtener más información sobre los repositorios y cómo configurarlas, consulte [configurar repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

## <a id="platforms"></a> Instalar a SQL Server 2017

Puede instalar SQL Server 2017 en Linux desde la línea de comandos. Para obtener instrucciones detalladas, consulte uno de los siguientes tutoriales:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalación en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-docker.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

Después de instalar, considere la posibilidad de realizar cambios de configuración adicionales para un rendimiento óptimo. Para obtener más información, consulte [procedimientos recomendados e instrucciones de configuración de SQL Server en Linux](sql-server-linux-performance-best-practices.md).

## <a id="sqlvnext"></a> Instalar la versión preliminar de SQL Server 2019

Puede instalar la versión preliminar de SQL Server 2019 en Linux con los mismos vínculos de inicio rápido en la sección anterior. Sin embargo, debe registrar el **Preview (vNext)** repositorio en lugar de la **CU** repositorio. Los tutoriales proporcionan instrucciones sobre cómo hacerlo.  

## <a id="upgrade"></a> Actualice SQL Server

Para actualizar el **mssql-server** a la versión más reciente del paquete, utilice uno de los siguientes comandos en función de su plataforma:

| Plataforma | Comandos de actualización del paquete |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

Estos comandos, descargue el paquete más reciente y reemplace los archivos binarios que se encuentran en `/opt/mssql/`. Las bases de datos generado por el usuario y las bases de datos del sistema no se ven afectados por esta operación.

> [!TIP]
> Si es primera [cambiar su repositorio configurado](sql-server-linux-change-repo.md), es posible que el **actualizar** comando para actualizar la versión de SQL Server. Esto sucede solo si la ruta de actualización se admite entre los dos repositorios.

## <a id="rollback"></a> Reversión SQL Server

Para revertir o degradación de SQL Server a una versión anterior, siga estos pasos:

1. Identifique el número de versión para el paquete de SQL Server que desea cambiar. Para obtener una lista de números de paquete, consulte el [notas de la versión](../linux/sql-server-linux-release-notes.md).

1. Cambiar a una versión anterior de SQL Server. En los siguientes comandos, reemplace `<version_number>` con el número de versión de SQL Server que identificó en el paso uno.

   | Plataforma | Comandos de actualización del paquete |
   |-----|-----|
   | RHEL | `sudo yum downgrade mssql-server-<version_number>.x86_64` |
   | SLES | `sudo zypper install --oldpackage mssql-server=<version_number>` |
   | Ubuntu | `sudo apt-get install mssql-server=<version_number>`<br/>`sudo systemctl start mssql-server` |

> [!NOTE]
> Solo se admite para degradar a una versión dentro de la misma versión principal, como SQL Server 2017.

## <a id="versioncheck"></a> Comprobar la versión instalada de SQL Server

Para comprobar la versión actual y la edición de SQL Server en Linux, use el procedimiento siguiente:

1. Si aún no está instalado, instale el [herramientas de línea de comandos de SQL Server](sql-server-linux-setup-tools.md).

1. Use **sqlcmd** para ejecutar un comando de Transact-SQL que muestra la versión de SQL Server y la edición.

   ```bash
   sqlcmd -S localhost -U SA -Q 'select @@VERSION'
   ```

## <a id="uninstall"></a> Desinstalar SQL Server

Para quitar el **mssql-server** empaquetar en Linux, use uno de los siguientes comandos en función de su plataforma:

| Plataforma | Comandos de eliminación de paquete |
|-----|-----|
| RHEL | `sudo yum remove mssql-server` |
| SLES | `sudo zypper remove mssql-server` |
| Ubuntu | `sudo apt-get remove mssql-server` |

Si quita el paquete no elimina los archivos de base de datos generada. Si desea eliminar los archivos de base de datos, use el siguiente comando:

```bash
sudo rm -rf /var/opt/mssql/
```

## <a id="unattended"></a> Instalación desatendida

Puede realizar una instalación desatendida de la siguiente manera:

- Siga los pasos de la inicial en el [inicios rápidos](#platforms) para registrar los repositorios e instalar SQL Server.
- Al ejecutar `mssql-conf setup`, establezca [variables de entorno](sql-server-linux-configure-environment-variables.md) y usar el `-n` (sin preguntar) opción.

En el ejemplo siguiente se configura la edición Developer de SQL Server con el **MSSQL_PID** variable de entorno. También acepta los términos de licencia (**ACCEPT_EULA**) y establece la contraseña del usuario SA (**MSSQL_SA_PASSWORD**). El `-n` parámetro realiza una instalación sin autorización del usuario donde se extraen los valores de configuración de las variables de entorno.

```bash
sudo MSSQL_PID=Developer ACCEPT_EULA=Y MSSQL_SA_PASSWORD='<YourStrong!Passw0rd>' /opt/mssql/bin/mssql-conf -n setup
```

También puede crear un script que lleva a cabo otras acciones. Por ejemplo, puede instalar otros paquetes de SQL Server.

Para obtener un script de ejemplo más detallado, vea los ejemplos siguientes:

- [Red Hat script de instalación desatendida](sample-unattended-install-redhat.md)
- [SUSE script de instalación desatendida](sample-unattended-install-suse.md)
- [Ubuntu script de instalación desatendida](sample-unattended-install-ubuntu.md)

## <a id="offline"></a> Instalación sin conexión

Si su equipo Linux no tiene acceso a los repositorios en línea que se usan en el [inicios rápidos](#platforms), puede descargar los archivos del paquete directamente. Estos paquetes se encuentran en el repositorio de Microsoft, [ https://packages.microsoft.com ](https://packages.microsoft.com).

> [!TIP]
> Si ha instalado correctamente mediante los pasos descritos en las guías de inicio rápido, no es necesario descargar o instalar manualmente los paquetes de SQL Server. En esta sección es solo para el escenario sin conexión.

1. **Descargue el paquete del motor de base de datos para su plataforma**. Buscar vínculos de descarga del paquete en la sección de detalles del paquete de la [notas de la versión](../linux/sql-server-linux-release-notes.md).

1. **Mover el paquete descargado a su equipo Linux**. Si usa un equipo diferente para descargar los paquetes, es una manera de mover los paquetes a la máquina Linux con la **scp** comando.

1. **Instalar el paquete del motor de base de datos**. Utilice uno de los siguientes comandos en función de la plataforma. Reemplace el nombre del archivo de paquete en este ejemplo con el nombre exacto que descargó.

   | Plataforma | Comando de instalación del paquete |
   |-----|-----|
   | RHEL | `sudo yum localinstall mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `sudo zypper install mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `sudo dpkg -i mssql-server_versionnumber_amd64.deb` |

    > [!NOTE]
    > También puede instalar los paquetes RPM (RHEL y SLES) con el `rpm -ivh` comando, pero los comandos en la tabla anterior instalan automáticamente dependencias si aprueban disponibles desde los repositorios.

1. **Resolver las dependencias que faltan**: Es posible que tenga dependencias que faltan en este momento. Si no es así, puede omitir este paso. En Ubuntu, si tiene acceso a repositorios aprobados que contiene esas dependencias, la solución más fácil es usar el `apt-get -f install` comando. Este comando también completa la instalación de SQL Server. Para inspeccionar manualmente las dependencias, use los siguientes comandos:

   | Plataforma | Mostrar dependencias (comando) |
   |-----|-----|
   | RHEL | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | SLES | `rpm -qpR mssql-server_versionnumber.x86_64.rpm` |
   | Ubuntu | `dpkg -I mssql-server_versionnumber_amd64.deb` |

   Después de resolver las dependencias que faltan, intente instalar de nuevo el paquete mssql-server.

1. **Completar la instalación de SQL Server**. Use **mssql-conf** para completar la instalación de SQL Server:

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

## <a name="licensing-and-pricing"></a>Precios y licencias

La licencia de SQL Server el mismo para Windows y Linux. Para obtener más información acerca de SQL Server, licencias y precios, consulte [licencias de SQL Server](https://www.microsoft.com/sql-server/sql-server-2017-pricing).

## <a name="optional-sql-server-features"></a>Características opcionales de SQL Server

Después de la instalación, también puede instalar o habilitar características opcionales de SQL Server.

- [Herramientas de línea de comandos de SQL Server](sql-server-linux-setup-tools.md)
- [Agente SQL Server](sql-server-linux-setup-sql-agent.md)
- [Búsqueda de texto completo de SQL Server](sql-server-linux-setup-full-text-search.md)
- [Machine Learning Services (R, Python)](sql-server-linux-setup-machine-learning.md)
- [SQL Server Integration Services](sql-server-linux-setup-ssis.md)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

> [!TIP]
> Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](sql-server-linux-faq.md).
