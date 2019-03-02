---
title: Notas de la versión de SQL Server 2017 en Linux | Microsoft Docs
description: Este artículo contiene las notas y características admitidas en SQL Server 2017 en Linux. Notas de la versión se incluyen para la versión más reciente y varias versiones anteriores.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/18/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: cd5c39f230db8fc72388d006fc17302956424633
ms.sourcegitcommit: 56fb7b648adae2c7b81bd969de067af1a2b54180
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/02/2019
ms.locfileid: "57227317"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de la versión de SQL Server 2017 en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Las notas siguientes se aplican a [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] que se ejecutan en Linux. Este artículo está dividido en secciones para cada versión. La versión de disponibilidad general (GA) incluye la compatibilidad detallada y los problemas conocidos. Cada actualización acumulativa (CU) o una versión de distribución general (GDR) tiene un vínculo a un artículo de soporte técnico que describe la CU de cambios, así como vínculos a la descargas de paquetes de Linux.

> [!TIP]
> Estas notas de la versión están diseñadas específicamente para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] libera. Para obtener más información sobre la nueva [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], consulte [notas de versión preliminar de SQL Server 2019 en Linux](sql-server-linux-release-notes-2019.md?view=sql-server-ver15).

## <a name="supported-platforms"></a>Plataformas compatibles

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Escritorio, servidor y estación de trabajo de Red Hat Enterprise Linux 7.3 o 7.4 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 y versiones posteriores on Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obtener más información, revise el [requisitos del sistema](sql-server-linux-setup.md#system) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux. Para la directiva de compatibilidad más reciente de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)], consulte el [directiva de soporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Herramientas

Herramientas de cliente más que tienen como destino [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] perfectamente puede tener como destino [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que se ejecutan en Linux. Algunas herramientas pueden tener un requisito de versión específica para funcionar bien con Linux. Para obtener una lista completa de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tools, vea [SQL herramientas y utilidades de SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Historial de versiones

La siguiente tabla enumera el historial de versiones para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].

| Versión               | Versión       | Fecha de la versión |
|-----------------------|---------------|--------------|
| [CU13](#CU13)         | 14.0.3048.4   | 2018-12-18   |
| [CU12](#CU12)         | 14.0.3045.24  | 2018-10-24   |
| [CU11](#CU11)         | 14.0.3038.14  | 2018-09-20   |
| [CU10](#CU10)         | 14.0.3037.1   | 2018-08-27   |
| [CU9-GDR2](#CU9-GDR2) | 14.0.3035.2   | 2018-08-18   |
| [GDR2](#GDR2)         | 14.0.2002.14  | 2018-08-18   |
| [CU9](#CU9)           | 14.0.3030.27  | 2018-07-18   |
| [CU8](#CU8)           | 14.0.3029.16  | 2018-06-21   |
| [CU7](#CU7)           | 14.0.3026.27  | 2018-05-24   |
| [CU6](#CU6)           | 14.0.3025.34  | 2018-04-19   |
| [CU5](#CU5)           | 14.0.3023.8   | 2018-03-20   |
| [CU4](#CU4)           | 14.0.3022.28  | 2018-02-20   |
| [CU3](#CU3)           | 14.0.3015.40  | 2018-01-03   |
| [GDR1](#GDR1)         | 14.0.2000.63  | 2018-01-03   |
| [CU2](#CU2)           | 14.0.3008.27  | 2017-11-28   |
| [CU1](#CU1)           | 14.0.3006.16  | 2017-10-24   |
| [GA](#GA)             | 14.0.1000.169 | 2017-10-02   |

## <a id="cuinstall"></a> Cómo instalar actualizaciones

Si ha configurado el repositorio CU (**mssql-server-2017**), se producirá la CU más reciente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] al realizar nuevas instalaciones de paquetes. El repositorio de CU es el valor predeterminado de todos los paquetes de artículos de instalación para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux. Si ha configurado el repositorio GDR (**mssql-server-2017-gdr**), solo recibirá actualizaciones de seguridad críticas desde la disponibilidad general. Si necesita CU de contenedor de Docker o actualizaciones GDR, consulte las imágenes oficiales de [Microsoft SQL Server en Linux para el motor de Docker](https://hub.docker.com/r/microsoft/mssql-server). Para obtener más información acerca de la configuración del repositorio, consulte [configurar repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

Si va a actualizar los existentes [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] paquetes, ejecute el comando de actualización adecuada para cada paquete obtener la CU más reciente. Para obtener instrucciones de actualización específica para cada paquete, consulte las guías de instalación siguientes:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar el paquete de búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Habilitar el Agente SQL Server](sql-server-linux-setup-sql-agent.md)

## <a id="CU13"></a> CU13 (diciembre de 2018)

Esta es la versión del 13 de actualización acumulativa (CU13) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3048.4. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4466404 ](https://support.microsoft.com/help/4466404).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3048.4-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3048.4-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3048.4-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a> CU12 (octubre de 2018)

Esta es la versión 12 de actualización acumulativa (CU12) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3045.24. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4464082 ](https://support.microsoft.com/help/4464082).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3045.24-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3045.24-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3045.24-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a> CU11 (septiembre de 2018)

Esta es la versión 11 de actualización acumulativa (CU11) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3038.14. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4462262 ](https://support.microsoft.com/help/4462262).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3038.14-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3038.14-2 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3038.14-2 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a> CU10 (agosto de 2018)

Esta es la versión de actualización acumulativa 10 (CU10) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3037.1. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4342123 ](https://support.microsoft.com/help/4342123).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3037.1-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3037.1-2 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3037.1-2 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a> CU9-GDR2 (agosto de 2018)

Ésta es una actualización de seguridad que también incluye la CU publicada anteriormente (CU9) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3035.2. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4293805 ](https://support.microsoft.com/help/4293805).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3035.2-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| Paquete RPM SLES | 14.0.3035.2-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3035.2-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a> GDR2 (agosto de 2018)

Se trata de una actualización de seguridad que solo incluye las correcciones de seguridad GDR2 (y GDR1) para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].  El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.2002.14. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4293803 ](https://support.microsoft.com/help/4293803).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.2002.14-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.2002.14-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.2002.14-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a> CU9 (julio de 2018)

Esta es la versión de actualización acumulativa 9 (CU9) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3030.27. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4341265 ](https://support.microsoft.com/help/4341265).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3030.27-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3030.27-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3030.27-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a> CU8 (junio de 2018)

Esta es la versión de actualización acumulativa 8 (CU8) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3029.16. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4338363 ](https://support.microsoft.com/help/4338363).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3029.16-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3029.16-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3029.16-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a> CU7 (mayo de 2018)

Esta es la versión de actualización acumulativa 7 (CU7) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3026.27. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4229789 ](https://support.microsoft.com/help/4229789).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3026.27-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3026.27-2 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3026.27-2 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a> CU6 (abril de 2018)

Esta es la versión 6 de actualización acumulativa (CU6) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3025.34. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4101464 ](https://support.microsoft.com/help/4101464).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3025.34-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3025.34-3 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3025.34-3 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a> CU5 (marzo de 2018)

Esta es la versión de actualización acumulativa 5 (CU5) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3023.8. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4092643 ](https://support.microsoft.com/help/4092643).

### <a name="known-upgrade-issue"></a>Problema conocido de actualización

Al actualizar desde una versión anterior a CU5, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podría no iniciarse con el siguiente error:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

Para resolver este error, habilite el Agente SQL Server y reiniciar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con los siguientes comandos:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3023.8-5 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3023.8-5 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3023.8-5 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a> CU4 (febrero de 2018)

Esta es la versión de actualización acumulativa 4 (CU4) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3022.28. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4056498 ](https://support.microsoft.com/help/4056498).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

> [!NOTE]
> A partir de CU4, Agente SQL Server ya no se instala como un paquete independiente. Se instala con el paquete del motor y debe estar habilitado para usar.

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3022.28-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3022.28-2 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3022.28-2 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a> GDR1 (enero de 2018)

Se trata de una actualización de seguridad que sólo incluya el GDR1 revisiones de seguridad de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.2000.63. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4057122 ](https://support.microsoft.com/help/4057122).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.2000.63-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.2000.63-3 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.2000.63-3 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a> CU3 (enero de 2018)

Esta es la versión de actualización acumulativa 3 (CU3) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3015.40. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4052987 ](https://support.microsoft.com/help/4052987).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3015.40-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3015.40-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3015.40-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Paquete de SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a> CU2 (noviembre de 2017)

Esta es la versión de actualización acumulativa 2 (CU2) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3008.27. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/4052574 ](https://support.microsoft.com/help/4052574).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3008.27-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3008.27-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3008.27-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Paquete de SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a> CU1 (octubre de 2017)

Esta es la versión de actualización acumulativa 1 (CU1) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.3006.16. Para obtener información acerca de las correcciones y mejoras en esta versión, consulte [ https://support.microsoft.com/help/KB4053439 ](https://support.microsoft.com/help/4038634).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3006.16-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.3006.16-3 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.3006.16-3 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Paquete de SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a> Disponibilidad general (octubre de 2017)

Esta es la versión de disponibilidad General (GA) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión para esta versión es 14.0.1000.169.

### <a name="package-details"></a>Detalles del paquete

En la tabla siguiente se muestran los detalles del paquete y ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no es necesario descargar estos paquetes directamente si usa los pasos en las siguientes guías de instalación:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md)
- [Instalar el paquete de búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar el paquete del Agente SQL Server](sql-server-linux-setup-sql-agent.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.1000.169-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Paquete de SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete RPM SLES | 14.0.1000.169-2 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de agente de SQL Server](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Paquete de Debian Ubuntu 16.04 | 14.0.1000.169-2 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Paquete de SQL Server Agent Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Paquete de SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a> Servicios y características no admitidas

Las siguientes características y servicios no están disponibles en Linux en el momento de la versión de GA. La compatibilidad de estas características se habilitarán cada vez más con el tiempo.

| Área | Característica no admitida o un servicio |
|-----|-----|
| **Motor de base de datos** | Replicación transaccional |
| &nbsp; | Replicación de mezcla |
| &nbsp; | Captura de datos modificados (vea Agente SQL Server) |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | Consulta distribuida con conexiones 3rd-party |
| &nbsp; | Servidores vinculados a orígenes de datos distinto [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | Sistema (XP_CMDSHELL, etcetera.) los procedimientos almacenados extendido |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | Establece los ensamblados CLR con EXTERNAL_ACCESS o permiso no seguro |
| &nbsp; | Buffer Pool Extension |
| **Agente SQL Server** |  Subsistemas: CmdExec, PowerShell, lectura de cola, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Agente de registro del LOG |
| &nbsp; | Captura de datos modificados (CDC) |
| &nbsp; | Copia de seguridad administrada |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| **Seguridad** | Administración extensible de claves |
| &nbsp; | Autenticación de Active Directory para los servidores vinculados | 
| &nbsp; | Autenticación de Active Directory para grupos de disponibilidad (AG) | 
| &nbsp; | herramientas de terceros AD 3rd (Powerbroker Centrify, Vintela) | 
| **Servicios** | SQL Server Browser |
| &nbsp; | SQL Server R services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | Coordinador de transacciones distribuidas (DTC) |

## <a name="known-issues"></a>Problemas conocidos

Las siguientes secciones describen los problemas conocidos con la versión de disponibilidad General (GA) de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] en Linux.

#### <a name="general"></a>General

- La longitud del nombre de host donde [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] está instalado necesita tener 15 caracteres o menos. 

    - **Resolución**: Cambie el nombre en/etc/hostname a algo de 15 caracteres como máximo.

- Establecer manualmente la hora del sistema con versiones anteriores en el tiempo provocará [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para detener la actualización de la hora del sistema interno dentro de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

    - **Resolución**: Reinicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Se admiten solo las instalaciones de instancia única.

    - **Resolución**: Si desea tener más de una instancia en un host determinado, considere el uso de las máquinas virtuales o contenedores de Docker. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Administrador de configuración no se puede conectar a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux.

- El idioma predeterminado de la **sa** inicio de sesión es el inglés.

    - **Resolución**: Cambiar el idioma de la **sa** inicio de sesión con la **ALTER LOGIN** instrucción.

#### <a name="databases"></a>Bases de datos

- No se puede mover la base de datos maestra con la utilidad mssql-conf. Otras bases de datos del sistema se pueden mover con mssql-conf.

- Al restaurar una base de datos que se hizo copia de seguridad [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Windows, debe usar el **WITH MOVE** cláusula en la instrucción de Transact-SQL.

- No se admiten las transacciones distribuidas que requieren el servicio Coordinador de transacciones distribuidas de Microsoft en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que se ejecutan en Linux. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se admiten servidores vinculados, a menos que implican el DTC. Para obtener más información, consulte [no se admiten las transacciones distribuidas que requieren el servicio Coordinador de transacciones distribuidas de Microsoft en SQL Server que se ejecutan en Linux](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Algunos algoritmos (conjuntos de cifrado) para la seguridad de capa de transporte (TLS) no funcionan correctamente con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux. Esto da como resultado errores de conexión al intentar conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], así como problemas para establecer conexiones entre las réplicas de grupos de alta disponibilidad.

   - **Resolución**: Modificar el **mssql.conf** script de configuración para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para deshabilitar conjuntos de cifrado problemático, haciendo lo siguiente:

      1. Agregue lo siguiente a /var/opt/mssql/mssql.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Reiniciar [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el siguiente comando.

      ```bash
      sudo systemctl restart mssql-server
      ```

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] no se puede restaurar las bases de datos en Windows que use OLTP en memoria en [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] en Linux. Para restaurar un [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] base de datos que utiliza OLTP en memoria, actualice primero las bases de datos [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] o [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] en Windows antes de moverlos a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux a través de la copia de seguridad o restaurar o adjuntar y separar.

- Permiso de usuario **ADMINISTER BULK OPERATIONS** no es compatible con Linux en este momento.

#### <a name="networking"></a>Redes

Las características que implican las conexiones TCP salientes desde el proceso sqlservr, como servidores vinculados o grupos de disponibilidad podrían no funcionar si se cumplen las dos condiciones siguientes:

1. El servidor de destino se especifica como un nombre de host y no una dirección IP.

1. La instancia de origen tiene IPv6 deshabilitado en el kernel. Para comprobar que si el sistema tiene IPv6 habilitada en el kernel, deben pasar todas las pruebas siguientes:

   - `cat /proc/cmdline` se imprimirá el cmdline de arranque del kernel actual. La salida no puede contener `ipv6.disable=1`.
   - / Proc/sys/net/ipv6/directorio debe existir.
   - Un programa de C que llama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` deben autenticarse correctamente: la syscall debe devolver un fd! = -1 y no se producirá un error con EAFNOSUPPORT.

El error exacto depende de la característica. Para los servidores vinculados, esto se manifiesta como un error de tiempo de espera de inicio de sesión. Para los grupos de disponibilidad, el `ALTER AVAILABILITY GROUP JOIN` DDL en la base de datos secundaria se producirá un error después de 5 minutos con un error de tiempo de espera de la configuración de descarga.

Para solucionar este problema, realice una de las siguientes acciones:

1. Use las direcciones IP en lugar de los nombres de host para especificar el destino de la conexión TCP.

1. Habilitar IPv6 en el kernel quitando `ipv6.disable=1` desde la línea de comandos de inicio. La manera de hacerlo depende de la distribución de Linux y el cargador de arranque, como grub. Si desea que IPv6 se deshabiliten, todavía puede deshabilitar estableciendo `net.ipv6.conf.all.disable_ipv6 = 1` en el `sysctl` configuración (por ejemplo, `/etc/sysctl.conf`). Esto todavía impedirá que el adaptador de red del sistema obtengan una dirección IPv6, pero permitir que funcionen las características de sqlservr.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Si usas **Network File System (NFS)** recursos compartidos remotos en producción, tenga en cuenta los siguientes requisitos de soporte técnico:

- Use la versión NFS **4.2 o superior**. Las versiones anteriores de NFS no admiten las características necesarias, como fallocate y creación del archivo disperso, comunes a los modernos sistemas de archivos.
- Busque sólo el **/var/opt/mssql** directorios en el montaje NFS. Otros archivos, tales como la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] archivos binarios del sistema, no se admiten.
- Asegúrese de que los clientes NFS usan la opción "nolock" al montar el recurso compartido remoto.

#### <a name="localization"></a>Localización

- Si no, la configuración regional es inglés (en_us) durante la instalación, debe usar la codificación UTF-8 en su sesión de bash o terminal. Si usa la codificación ASCII, es posible que vea un error similar al siguiente:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Si no se puede utilizar la codificación UTF-8, ejecute la instalación mediante la variable de entorno MSSQL_LCID para especificar la opción de lenguaje.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Cuando se ejecuta el programa de instalación de mssql-conf y realizar una instalación distinta del inglés de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], caracteres extendidos incorrectos se muestran después del texto localizado, "Configuración de SQL Server …". O bien, para las instalaciones en función de no latinos, podría faltar la oración completamente. La frase que faltan debe mostrar la cadena localizada siguiente: "El PID de licencias se ha procesado correctamente. La nueva edición es [\<nombre\> edition] ". Esta cadena es la salida de únicamente con fines informativos y los próximos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] actualización acumulativa lo solucionará todos los idiomas. Esto no afecta a la instalación correcta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de ninguna manera. 

#### <a name="full-text-search"></a>Búsqueda de texto completo

- No todos los filtros están disponibles con esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros admitidos, consulte [instalar búsqueda de texto completo de SQL Server en Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- El **mssql-server-es** paquete no se admite en SUSE en esta versión. Se admite actualmente en Ubuntu y en Red Hat Enterprise Linux (RHEL).

- Con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] actualizar los Linux CTP 2.1 y versiones posteriores, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] paquetes pueden utilizar conexiones de ODBC en Linux. Esta funcionalidad se ha probado con el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y los controladores ODBC de MySQL, pero también se espera que funcione con cualquier controlador ODBC Unicode que cumple la especificación de ODBC. En tiempo de diseño, puede proporcionar un DSN o una cadena de conexión para conectarse a los datos ODBC; También puede usar la autenticación de Windows. Para obtener más información, consulte el [entrada de blog de anuncio de compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Las siguientes características no se admiten en esta versión, al ejecutar paquetes SSIS en Linux:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Base de datos de catálogo
  - Ejecución del paquete programado por el Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Captura de datos modificados (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Escalar horizontalmente
  - Azure Feature Pack para SSIS
  - Compatibilidad con Hadoop y HDFS
  - Microsoft Connector for SAP BW

Para obtener una lista de componentes integrados de SSIS que no se admiten actualmente o que son compatibles con limitaciones, consulte [limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md#components).

Para obtener más información acerca de SSIS en Linux, consulte los artículos siguientes:
-   [Blog que anuncia la compatibilidad con SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SQL Server Management Studio (SSMS)

Las siguientes limitaciones se aplican a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] en Windows conectado a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux.

- No se admiten los planes de mantenimiento.

- Almacén de administración de datos (MDW) y el recopilador de datos en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no se admiten. 

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] Los componentes de interfaz de usuario con autenticación de Windows o las opciones de registro de eventos de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como los inicios de sesión SQL. 

- No se puede modificar el número de archivos de registro para conservar.

## <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los tutoriales siguientes:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)
- [Ejecución y conexión: nube](quickstart-install-connect-clouds.md)

Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](sql-server-linux-faq.md).
