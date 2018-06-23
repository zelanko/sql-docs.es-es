---
title: Notas de la versión de SQL Server 2017 en Linux | Documentos de Microsoft
description: Este artículo contiene las notas de la versión y características admitidas en SQL Server 2017 ejecutando en Linux. Notas de la versión se incluyen con la versión más reciente y varias versiones anteriores.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/20/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 4762570a478ca6ba6dcaab5e0f7b3e2984f849cf
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312213"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de la versión de SQL Server 2017 en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Las siguientes notas de versión se aplican a SQL Server 2017 para Linux. Este artículo está dividido en secciones para cada versión. La versión de disponibilidad general (GA) incluye la compatibilidad detallada y los problemas conocidos. Cada versión de actualización acumulativa (CU) tiene un vínculo a un tema de soporte técnico en el que se describen los cambios en la CU, así como vínculos a las descargas de paquetes de Linux.

## <a name="supported-platforms"></a>Plataformas compatibles

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 o 7.4 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| Service Pack 2 SUSE Enterprise Linux Server v12 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obtener más información, revise la [requisitos del sistema](sql-server-linux-setup.md#system) para SQL Server en Linux. Para la directiva de soporte técnico más reciente para SQL Server 2017, consulte el [directiva de soporte técnico de Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Herramientas

La mayoría herramientas de cliente existente que tengan como destino de SQL Server sin problemas pueden acceder a SQL Server que se ejecutan en Linux. Algunas herramientas pueden tener un requisito de versión específica que funcionen bien con Linux. Para obtener una lista completa de herramientas de SQL Server, vea [SQL herramientas y utilidades de SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Historial de versiones

En la tabla siguiente se enumera el historial de versiones de SQL Server 2017.

| Versión | Versión | Fecha de lanzamiento |
|-----|-----|-----|
| [CU8](#CU8) | 14.0.3029.16 | 6-2018 |
| [CU7](#CU7) | 14.0.3026.27 | 2018 5 |
| [CU6](#CU6) | 14.0.3025.34 | 4-2018 |
| [CU5](#CU5) | 14.0.3023.8 | 3-2018 |
| [CU4](#CU4) | 14.0.3022.28 | 2-2018 |
| [CU3](#CU3) | 14.0.3015.40 | 1-2018 |
| [CU2](#CU2) | 14.0.3008.27 | 11-2017 |
| [CU1](#CU1) | 14.0.3006.16 | 10-2017 |
| [GA](#GA) | 14.0.1000.169 | 10-2017 |

## <a id="cuinstall"></a> Cómo instalar actualizaciones acumulativas

Si ha configurado el repositorio de la actualización acumulativa, obtendrá la actualización acumulativa más reciente de los paquetes de SQL Server al realizar nuevas instalaciones. El repositorio de actualización acumulativa es el valor predeterminado para todos los artículos de la instalación de paquetes de SQL Server en Linux. Para obtener más información acerca de la configuración del repositorio, consulte [configurar repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

Si va a actualizar los paquetes existentes de SQL Server, ejecute el comando de actualización apropiada para cada paquete obtener la actualización acumulativa más reciente. Para obtener instrucciones de actualización específica para cada paquete, consulte las guías de instalación siguientes:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar el paquete de la búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Habilitar el Agente SQL Server](sql-server-linux-setup-sql-agent.md)

## <a id="CU8"></a> CU8 (mayo de 2018)

Se trata de la versión 8 de actualización acumulativa (CU8) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.3029.16. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/en-us/help/4229789 ](https://support.microsoft.com/en-us/help/4229789).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3029.16-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3029.16-1 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3029.16-1 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7 (mayo de 2018)

Se trata de la versión de la actualización acumulativa 7 (CU7) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.3026.27. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/en-us/help/4229789 ](https://support.microsoft.com/en-us/help/4229789).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3026.27-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3026.27-2 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3026.27-2 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6 (abril de 2018)

Se trata de la versión de la actualización acumulativa 6 (CU6) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.3025.34. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3025.34-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3025.34-3 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3025.34-3 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (marzo de 2018)

Se trata de la versión 5 de actualización acumulativa (CU5) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.3023.8. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4092643 ](https://support.microsoft.com/help/4092643).

### <a name="known-upgrade-issue"></a>Problema de actualización conocido

Al actualizar desde una versión anterior a CU5, SQL Server no puede iniciarse con el siguiente error:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

Para resolver este error, habilite el Agente SQL Server y reinicie SQL Server con los siguientes comandos:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3023.8-5 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3023.8-5 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3023.8-5 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (febrero de 2018)

Se trata de la versión de actualización acumulativa 4 (CU4) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.3022.28. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/en-us/help/4056498 ](https://support.microsoft.com/en-us/help/4056498).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

> [!NOTE]
> A partir de CU4, Agente SQL Server ya no se instala como un paquete independiente. Se instala con el paquete de motor y debe estar habilitado para usar.

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3022.28-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3022.28-2 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3022.28-2 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU3"></a> CU3 (enero de 2018)

Se trata de la versión de la actualización acumulativa 3 (CU3) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.3015.40. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/en-us/help/4052987 ](https://support.microsoft.com/en-us/help/4052987).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3015.40-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3015.40-1 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3015.40-1 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (noviembre de 2017)

Se trata de la versión de la actualización acumulativa 2 (CU2) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.3008.27. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4052574 ](https://support.microsoft.com/help/4052574).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3008.27-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3008.27-1 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3008.27-1 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (octubre de 2017)

Se trata de la versión de actualización acumulativa 1 (CU1) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.3006.16. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/KB4053439 ](https://support.microsoft.com/help/4038634).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3006.16-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3006.16-3 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3006.16-3 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> GA (octubre de 2017)

Se trata de la versión de disponibilidad general (GA) de SQL Server 2017. La versión del motor de SQL Server para esta versión es 14.0.1000.169.

### <a name="package-details"></a>Detalles del paquete

En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos en las siguientes guías de instalación:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md)
- [Instalar el paquete de la búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar el paquete del Agente SQL Server](sql-server-linux-setup-sql-agent.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.1000.169-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.1000.169-2 | [paquete de RPM del motor de servidor MSSQL](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.1000.169-2 | [Motor de paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Paquete SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> Servicios y características no admitidas

Las siguientes características y servicios no están disponibles en Linux en el momento de la versión de GA. La compatibilidad de estas características se habilitarán cada vez más con el tiempo.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **motor de base de datos** | Replicación transaccional |
| &nbsp; | Replicación de mezcla |
| &nbsp; | Stretch DB |
| &nbsp; | Polybase |
| &nbsp; | Consulta distribuida con conexiones 3ª parte |
| &nbsp; | Servidores vinculados a orígenes de datos distintos de SQL Server |
| &nbsp; | (XP_CMDSHELL, etcetera) los procedimientos almacenados extendidos del sistema |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | Conjunto de ensamblados CLR con EXTERNAL_ACCESS o UNSAFE permiso |
| &nbsp; | Buffer Pool Extension |
| **Agente SQL Server** |  Subsistemas: CmdExec, PowerShell, lector de cola, SSIS, SSAS, SSRS |
| &nbsp; | Trabajos |
| &nbsp; | Agente de registro del LOG |
| &nbsp; | Captura de datos modificados |
| &nbsp; | Copia de seguridad administrada |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| **Seguridad** | Administración extensible de claves |
| &nbsp; | Autenticación de Active Directory para los servidores vinculados | 
| &nbsp; | Autenticación de Active Directory para grupos de disponibilidad (AG) | 
| &nbsp; | herramientas de terceros AD 3rd (Centrify, Vintela, Powerbroker) | 
| **Servicios** | SQL Server Browser |
| &nbsp; | Servicios de SQL Server R |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | Coordinador de transacciones distribuidas (DTC) |

## <a name="known-issues"></a>Problemas conocidos

En las siguientes secciones se describen los problemas conocidos con la versión de disponibilidad General (GA) de SQL Server 2017 en Linux.

#### <a name="general"></a>General

- Se admiten actualizaciones a la versión de GA de SQL Server 2017 de CTP 2.1 o superior. 

- La longitud del nombre de host donde SQL Server está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: cambiar el nombre de host/etcetera/a algo 15 caracteres como máximo.

- Establecer manualmente la hora del sistema con las versiones anteriores en el tiempo, harán que SQL Server detener la actualización de la hora del sistema interno de SQL Server.

    - **Resolución**: reinicie SQL Server.

- Se admiten sólo las instalaciones de instancia única.

    - **Resolución**: si desea tener más de una instancia en un host determinado, considere el uso de máquinas virtuales o contenedores de Docker. 

- Administrador de configuración de SQL Server no se puede conectar a SQL Server en Linux.

- El idioma predeterminado de la **sa** inicio de sesión es el inglés.

    - **Resolución**: cambiar el idioma de la **sa** inicio de sesión con la **ALTER LOGIN** instrucción.

#### <a name="databases"></a>Bases de datos

- No se puede mover la base de datos maestra con la utilidad mssql-conf. Otras bases de datos del sistema pueden aplicarse con mssql-conf.

- Al restaurar una base de datos que se copió en SQL Server en Windows, debe utilizar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux. SQL Server a SQL Server se admiten servidores vinculados a menos que implican el DTC. Para obtener más información, consulte [no se admiten las transacciones distribuidas que requiera el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Algunos algoritmos (conjuntos de cifrado) para la seguridad de capa de transporte (TLS) no funcionan correctamente con SQL Server en Linux. Esto da como resultado errores de conexión al intentar conectarse a SQL Server, así como problemas para establecer conexiones entre réplicas en los grupos de alta disponibilidad.

   - **Resolución**: modificar el **mssql.conf** script de configuración de SQL Server en Linux para deshabilitar conjuntos de cifrado problemático, mediante las acciones siguientes:

      1. Agregue lo siguiente al /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Reinicie SQL Server con el siguiente comando.

      ```bash
      sudo systemctl restart mssql-server
      ```

- No se puede restaurar las bases de datos de SQL Server 2014 en Windows que use OLTP en memoria en SQL Server 2017 en Linux. Para restaurar una base de datos de SQL Server 2014 que utiliza OLTP en memoria, actualizar las bases de datos a SQL Server 2016 o 2017 de SQL Server en Windows antes de pasar a SQL Server en Linux a través de copia de seguridad/restauración o separar y adjuntar.

- Permiso de usuario **ADMINISTER BULK OPERATIONS** no se admite en Linux en este momento.

#### <a name="networking"></a>Redes

Características que implican las conexiones TCP salientes desde el proceso sqlservr, como servidores vinculados o grupos de disponibilidad, podrían no funcionar si se cumplen las dos condiciones siguientes:

1. El servidor de destino se especifica como un nombre de host y no una dirección IP.

1. La instancia de origen tiene IPv6 deshabilitado en el kernel. Para comprobar que si el sistema tiene IPv6 habilitada en el kernel, deben pasar todas las pruebas siguientes:

   - `cat /proc/cmdline` se imprimirá el cmdline de arranque del núcleo actual. El resultado no debe contener `ipv6.disable=1`.
   - Sys/proc / / net/ipv6/directorio debe existir.
   - Un programa de C que llama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` debe ejecutarse correctamente: la syscall debe devolver un fd! = -1 y no producirá un error con EAFNOSUPPORT.

El error exacto depende de la característica. Para los servidores vinculados, esto se manifiesta como un error de tiempo de espera de inicio de sesión. Para los grupos de disponibilidad, el `ALTER AVAILABILITY GROUP JOIN` DDL en la base de datos secundaria se producirá un error después de 5 minutos con un error de tiempo de espera de configuración de descarga.

Para solucionar este problema, realice una de las siguientes acciones:

1. Usar direcciones IP en lugar de los nombres de host para especificar el destino de la conexión TCP.

1. Habilitar IPv6 en el kernel quitando `ipv6.disable=1` desde la línea de comandos de arranque. La manera de hacerlo depende de la distribución de Linux y el cargador de arranque, como grub. Si desea IPv6 que se deshabilite, todavía puede deshabilitar estableciendo `net.ipv6.conf.all.disable_ipv6 = 1` en el `sysctl` configuración (por ejemplo, `/etc/sysctl.conf`). Esto se sigue impedir que el adaptador de red del sistema entre una dirección IPv6, pero permitir que funcionen las características de sqlservr.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Si usa **Network File System (NFS)** recursos compartidos remotos en producción, tenga en cuenta los siguientes requisitos de soporte técnico:

- Utilice la versión NFS **4.2 o posterior**. Las versiones anteriores de NFS son compatibles con las características necesarias, como fallocate y la creación de archivos dispersos, comunes a sistemas de archivos modernos.
- Busque sólo el **/var/opt/mssql** directorios en el montaje NFS. No se admiten otros archivos, como los archivos binarios del sistema de SQL Server.
- Asegúrese de que los clientes NFS usan la opción 'nolock' al montar el recurso compartido remoto.

#### <a name="localization"></a>Localización

- Si no, la configuración regional es inglés (en_us) durante la instalación, debe usar la codificación UTF-8 en su sesión intensiva de errores/terminal. Si utiliza la codificación ASCII, verá un mensaje de error similar al siguiente:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Si no puede utilizar la codificación UTF-8, ejecute el programa de instalación mediante la variable de entorno MSSQL_LCID para especificar la opción de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Cuando ejecuta el programa de instalación de mssql-conf y realizar una instalación distinta del inglés de SQL Server, incorrecto caracteres extendidos se muestran después del texto localizado, "Configuración de SQL Server …". O bien, para las instalaciones en función de no latinos, podría faltar la frase completamente. La frase que faltan debería mostrar la cadena adaptada siguiente: "el PID de licencia se procesó correctamente.  Es la nueva edición [\<nombre\> edición] ". Esta cadena se genera solo para fines informativos y la actualización acumulativa del servidor SQL siguiente solucionará para todos los idiomas. Esto no afecta a la instalación correcta de SQL Server en modo alguno. 

#### <a name="full-text-search"></a>Búsqueda de texto completo

- No todos los filtros están disponibles con esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros admitidos, consulte [instalar búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- El **mssql server es** paquete no es compatible con SUSE en esta versión. Se admite actualmente en Ubuntu y en Red Hat Enterprise Linux (RHEL).

- Con SSIS al actualizar los Linux CTP 2.1 y versiones posteriores, paquetes SSIS pueden usar conexiones de ODBC en Linux. Esta funcionalidad se ha probado con el servidor SQL Server y los controladores ODBC de MySQL, pero también se espera que funcione con cualquier controlador de ODBC Unicode que se ajusta a la especificación de ODBC. En tiempo de diseño, puede proporcionar un DSN o una cadena de conexión para conectarse a los datos ODBC; También puede utilizar la autenticación de Windows. Para obtener más información, consulte el [entrada del blog del anuncio de compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Las siguientes características no se admiten en esta versión, al ejecutar paquetes SSIS en Linux:
  - Base de datos de catálogo de SSIS
  - Ejecución del paquete programado por el Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Captura de datos modificados (CDC)
  - Ampliación SSIS
  - Feature Pack de Azure para SSIS
  - Compatibilidad con Hadoop y HDFS
  - Microsoft Connector for SAP BW

Para obtener una lista de componentes SSIS integrados que no son compatibles actualmente o que son compatibles con limitaciones, vea [limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md#components).

Para obtener más información sobre SSIS en Linux, consulte los artículos siguientes:
-   [Anuncio de entrada de blog compatibilidad con SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)

#### <a name="-a-idssmsa-sql-server-management-studio-ssms"></a>< un Id. = "ssms" ></a> SQL Server Management Studio (SSMS)

Las siguientes limitaciones se aplican a SSMS en Windows conectados a SQL Server en Linux.

- No se admiten los planes de mantenimiento.

- Almacén de datos de administración (MDW) y el recopilador de datos en SSMS no son compatibles. 

- Componentes de SSMS UI con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- No se puede modificar el número de archivos de registro que se va a conservar.

## <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los siguientes tutoriales:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [Ejecución y conexión: nube](quickstart-install-connect-clouds.md)

Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](sql-server-linux-faq.md).
