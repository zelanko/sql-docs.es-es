---
title: Instalar SQL Server de 2017 en Linux | Documentos de Microsoft
description: "Instalar, actualizar y desinstalar SQL Server en Linux. En este tema se trata los escenarios de en línea, sin conexión y desatendidos."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 08/28/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 565156c3-7256-4e63-aaf0-884522ef2a52
ms.translationtype: MT
ms.sourcegitcommit: 303d3b74da3fe370d19b7602c0e11e67b63191e7
ms.openlocfilehash: f746037f695301881ce9a993f3d556db44f44292
ms.contentlocale: es-es
ms.lasthandoff: 08/29/2017

---
# <a name="installation-guidance-for-sql-server-on-linux"></a>Guía de instalación para SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tema se explica cómo instalar, actualizar y desinstalar SQL Server 2017 en Linux. SQL Server de 2017 RC2 es compatible con Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) y Ubuntu. También está disponible como una imagen de Docker, que se puede ejecutar en el motor de Docker en Linux o Docker para Windows y Mac.

> [!TIP]
> Para empezar a trabajar rápidamente, saltar a uno de los tutoriales de inicio rápido para [RHEL](quickstart-install-connect-red-hat.md), [SLES](quickstart-install-connect-suse.md), [Ubuntu](quickstart-install-connect-ubuntu.md), o [Docker](quickstart-install-connect-docker.md).

## <a id="supportedplatforms"></a>Plataformas compatibles

SQL Server 2017 es compatible con las siguientes plataformas de Linux:

| Plataforma | Versiones admitidas | Obtener
|-----|-----|-----
| **Red Hat Enterprise Linux** | 7.3 | [Obtener RHEL 7.3](http://access.redhat.com/products/red-hat-enterprise-linux/evaluation)
| **SUSE Linux Enterprise Server** | SP2 de V12 | [Obtener el Service Pack 2 SLES v12](https://www.suse.com/products/server)
| **Ubuntu** | 16.04 | [Obtener Ubuntu 16.04](http://www.ubuntu.com/download/server)
| **Motor de docker** | 1.8+ | [Obtener Docker](http://www.docker.com/products/overview)

## <a id="system"></a>Requisitos del sistema

SQL Server 2017 tiene los siguientes requisitos de sistema para Linux:

|||
|-----|-----|
| **Memoria** | 3,25 GB |
| **Sistema de archivos** | **XFS** o **EXT4** (sí los sistemas de archivos, como **BTRFS**, no son compatibles) |
| **Espacio en disco** | 6 GB |
| **Velocidad del procesador** | 2 GHz |
| **Núcleos de procesador** | 2 núcleos |
| **Tipo de procesador** | solo x64 compatible |

> [!NOTE]
> Motor de SQL Server ha sido probado hasta 1 TB de memoria en este momento.

## <a id="platforms"></a> Instalar SQL Server

Puede instalar a SQL Server en Linux desde la línea de comandos. Para obtener instrucciones, consulte uno de los siguientes tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-docker.md)

## <a id="upgrade"></a>Actualizar SQL Server

Para actualizar la **mssql server** el paquete a la versión más reciente, use uno de los siguientes comandos en función de la plataforma:

| Plataforma | Comandos de actualización de paquete |
|-----|-----|
| RHEL | `sudo yum update mssql-server` |
| SLES GRANDE | `sudo zypper update mssql-server` |
| Ubuntu | `sudo apt-get update`<br/>`sudo apt-get install mssql-server` |

Descargar el paquete más reciente de estos comandos y reemplace los binarios que se encuentran en `/opt/mssql/`. Las bases de datos generado por el usuario y las bases de datos del sistema no se ven afectados por esta operación.

## <a id="rollback"></a>Revertir SQL Server

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

> [!IMPORTANT]
> Degradación solo se admite entre RC2 y RC1 en este momento.

## <a id="uninstall"></a>Desinstalar SQL Server

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

## <a id="unattended"></a>Instalación desatendida

Puede realizar una instalación desatendida de la manera siguiente:

- Siga los pasos de la inicial de la [tutoriales de inicio rápido de](#platforms) para registrar los repositorios e instalar SQL Server.
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

## <a id="offline"></a>Instalación sin conexión

Si su equipo Linux no tiene acceso a los repositorios en línea que se utiliza en el [rápidas](#platforms), puede descargar los archivos del paquete directamente. Estos paquetes se encuentran en el repositorio de Microsoft, [https://packages.microsoft.com](https://packages.microsoft.com).

> [!TIP]
> Si se ha instalado correctamente con los pasos descritos en las guías de inicio rápidos, no es necesario descargar o instalar manualmente los paquetes siguientes. Esta sección es solo para el escenario sin conexión.

1. **Descargue el paquete de motor de base de datos para su plataforma**. Buscar vínculos de descarga de paquete en la sección de detalles del paquete de la [notas de la versión](sql-server-linux-release-notes.md).

1. **Mover el paquete descargado en el equipo Linux**. Si utiliza un equipo diferente para descargar los paquetes, es una manera de mover los paquetes a su equipo Linux con el **scp** comando.

1. **Instalar el paquete del motor de base de datos**. Utilice uno de los siguientes comandos en función de la plataforma. Reemplace el nombre de archivo de paquete en este ejemplo con el nombre exacto que se descargó.

   | Plataforma | Comando de eliminación de paquete |
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

## <a name="next-steps"></a>Pasos siguientes

Después de la instalación, también puede instalar otros paquetes de SQL Server opcionales.

- [Herramientas de línea de comandos de SQL Server](sql-server-linux-setup-tools.md)
- [Agente SQL Server](sql-server-linux-setup-sql-agent.md)
- [Búsqueda de texto completo de SQL Server](sql-server-linux-setup-full-text-search.md)
- [Servicios de integración de SQL Server (Ubuntu)](sql-server-linux-setup-ssis.md)

Conectarse a la instancia de SQL Server para empezar a crear y administrar bases de datos. Para empezar, vea los tutoriales de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)

