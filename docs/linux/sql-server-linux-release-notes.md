---
title: Notas de la versión de SQL Server 2017 en Linux
description: Este artículo contiene las notas de la versión y las características admitidas para SQL Server 2017 que se ejecutan en Linux. Las notas de la versión se incluyen en la versión más reciente y en varias versiones anteriores.
author: VanMSFT
ms.author: vanto
ms.date: 06/25/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: 5b6fce0bdde7e320eea0371125a61627652de80d
ms.sourcegitcommit: d667fa9d6f1c8035f15fdb861882bd514be020d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68388413"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas de la versión de SQL Server 2017 en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Las siguientes notas de la versión [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] se aplican a la ejecución en Linux. Este artículo está dividido en secciones para cada versión. La versión de disponibilidad general (GA) incluye la compatibilidad detallada y los problemas conocidos. Cada actualización acumulativa (CU) o versión de distribución general (GDR) tiene un vínculo a un artículo de soporte que describe los cambios de la CU, así como los vínculos a las descargas de paquetes de Linux.

> [!TIP]
> Estas notas de la versión son [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] específicas para las versiones. Para obtener más información sobre el [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]nuevo, consulte las [notas de la versión de SQL Server 2019 Preview en Linux](sql-server-linux-release-notes-2019.md?view=sql-server-ver15).

## <a name="supported-platforms"></a>Plataformas compatibles

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Red Hat Enterprise Linux 7,3, 7,4, 7,5 o 7,6 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de Docker 1.8 + en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obtener más información, revise los [requisitos del sistema](sql-server-linux-setup.md#system) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux. Para ver la Directiva de soporte [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]técnico más reciente de, consulte la [Directiva de soporte técnico de Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Herramientas

La mayoría de las herramientas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cliente existentes que tienen [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como destino se pueden ejecutar sin problemas en Linux. Algunas herramientas pueden tener un requisito de versión específico para funcionar bien con Linux. Para obtener una lista completa [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de las herramientas, vea [herramientas y utilidades de SQL para obtener SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Historial de versiones

En la tabla siguiente se muestra el historial [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de versiones de.

| Release               | `Version`       | Fecha de la versión |
|-----------------------|---------------|--------------|
| [CU15](#CU15)         | 14.0.3162.1   | 2019-05-23   |
| [CU14](#CU14)         | 14.0.3076.1   | 2019-03-25   |
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

## <a id="cuinstall"></a>Cómo instalar actualizaciones

Si ha configurado el repositorio Cu (**MSSQL-Server-2017**), obtendrá la última cu de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] los paquetes al realizar nuevas instalaciones. El repositorio cu es el valor predeterminado para todos los artículos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instalación de paquetes para en Linux. Si ha configurado el repositorio de GDR (**MSSQL-Server-2017-GDR**), solo obtendrá actualizaciones de seguridad críticas publicadas desde la fecha de disponibilidad general. Si necesita actualizaciones de CU o GDR del contenedor de Docker, consulte las imágenes oficiales de [Microsoft SQL Server en Linux para el motor de Docker](https://hub.docker.com/r/microsoft/mssql-server). Para obtener más información sobre la configuración del repositorio, consulte [configuración de repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

Si está actualizando paquetes [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] existentes, ejecute el comando de actualización adecuado para cada paquete para obtener la cu más reciente. Para obtener instrucciones de actualización específicas para cada paquete, vea las guías de instalación siguientes:

- [Instalar paquete de SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar paquete de búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Habilitar Agente SQL Server](sql-server-linux-setup-sql-agent.md)

## <a id="CU15"></a>CU15 (2019 de mayo)

Esta es la versión de actualización acumulativa 15 (CU15) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3162.1. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/en-us/help/4498951](https://support.microsoft.com/en-us/help/4498951)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3162.1-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3162.1-1 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3162.1-1 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU14"></a>CU14 (2019)

Esta es la versión de actualización acumulativa 14 (CU14) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3076.1. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3076.1-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3076.1-2 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3076.1-2 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU13"></a>CU13 (Dec 2018)

Esta es la versión de actualización acumulativa 13 (CU13) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3048.4. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3048.4-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3048.4-1 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3048.4-1 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU12"></a>CU12 (2018 de octubre)

Esta es la versión de actualización acumulativa 12 (CU12) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3045.24. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3045.24-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3045.24-1 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3045.24-1 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU11"></a>CU11 (2018 de septiembre)

Esta es la versión de actualización acumulativa 11 (CU11) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3038.14. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3038.14-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3038.14-2 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3038.14-2 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU10"></a>CU10 (2018 de agosto)

Esta es la versión de actualización acumulativa 10 (CU10) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3037.1. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3037.1-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3037.1-2 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3037.1-2 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU9-GDR2"></a>CU9-GDR2 (2018 de agosto)

Se trata de una actualización de seguridad que también incluye la CU publicada anteriormente (CU9 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]) para. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3035.2. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3035.2-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| Paquete de SLES RPM | 14.0.3035.2-1 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3035.2-1 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a id="GDR2"></a>GDR2 (2018 de agosto)

Se trata de una actualización de seguridad que solo incluye las correcciones de seguridad de GDR2 [!INCLUDE[ssSQL17](../includes/sssql17-md.md)](y GDR1) para.  La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.2002.14. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.2002.14-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.2002.14-1 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.2002.14-1 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a id="CU9"></a>CU9 (Jul 2018)

Esta es la versión de actualización acumulativa 9 (CU9) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3030.27. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3030.27-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3030.27-1 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3030.27-1 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU8"></a>CU8 (2018 de junio)

Esta es la versión de actualización acumulativa 8 (CU8) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3029.16. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3029.16-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3029.16-1 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3029.16-1 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU7"></a>CU7 (2018 de mayo)

Esta es la versión de actualización acumulativa 7 (CU7) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3026.27. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3026.27-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3026.27-2 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3026.27-2 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU6"></a>CU6 (2018 de abril)

Esta es la versión de actualización acumulativa 6 (CU6) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3025.34. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3025.34-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3025.34-3 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3025.34-3 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU5"></a>CU5 (2018 de marzo)

Esta es la versión de actualización acumulativa 5 (CU5) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3023.8. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643)versión, vea.

### <a name="known-upgrade-issue"></a>Problema de actualización conocido

Cuando se actualiza desde una versión anterior a CU5, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] podría no iniciarse con el siguiente error:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

Para resolver este error, habilite Agente SQL Server y reinicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con los siguientes comandos:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3023.8-5 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3023.8-5 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3023.8-5 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU4"></a>CU4 (2018 de febrero)

Esta es la versión de actualización acumulativa 4 (CU4) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3022.28. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

> [!NOTE]
> A partir de CU4, Agente SQL Server ya no se instala como un paquete independiente. Se instala con el paquete del motor y debe estar habilitado para su uso.

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3022.28-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3022.28-2 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3022.28-2 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GDR1"></a>GDR1 (Ene 2018)

Se trata de una actualización de seguridad que solo incluye las correcciones [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de seguridad de GDR1 para. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.2000.63. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.2000.63-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.2000.63-3 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.2000.63-3 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a id="CU3"></a>CU3 (Ene 2018)

Esta es la versión de actualización acumulativa 3 (CU3) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3015.40. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3015.40-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Paquete de Agente SQL Server RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3015.40-1 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Paquete de Agente SQL Server RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3015.40-1 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Agente SQL Server paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU2"></a>CU2 (2017 de noviembre)

Esta es la versión de actualización acumulativa 2 (CU2) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3008.27. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3008.27-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Paquete de Agente SQL Server RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3008.27-1 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Paquete de Agente SQL Server RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3008.27-1 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Agente SQL Server paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="CU1"></a>CU1 (2017 de octubre)

Esta es la versión de actualización acumulativa 1 (CU1) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.3006.16. Para obtener información acerca de las correcciones y mejoras de esta [https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634)versión, vea.

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.3006.16-3 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Paquete de Agente SQL Server RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.3006.16-3 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Paquete de Agente SQL Server RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.3006.16-3 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Agente SQL Server paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a id="GA"></a>GA (2017 de octubre)

Esta es la versión de disponibilidad general (GA) [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]de. La [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] versión de esta versión es 14.0.1000.169.

### <a name="package-details"></a>Detalles del paquete

En la tabla siguiente se enumeran los detalles del paquete y las ubicaciones de descarga de los paquetes RPM y Debian. Tenga en cuenta que no necesita descargar estos paquetes directamente si usa los pasos de las siguientes guías de instalación:

- [Instalar paquete de SQL Server](sql-server-linux-setup.md)
- [Instalar paquete de búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar paquete de Agente SQL Server](sql-server-linux-setup-sql-agent.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 14.0.1000.169-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete de Agente SQL Server RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Paquete SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Paquete de SLES RPM | 14.0.1000.169-2 | [MSSQL-paquete de RPM de motor de servidor](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Paquete RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Paquete de Agente SQL Server RPM](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Paquete Ubuntu 16,04 Debian | 14.0.1000.169-2 | [Paquete Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Paquete Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Paquete Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Agente SQL Server paquete Debian](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Paquete SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="Unsupported"></a>Características no admitidas & servicios

Las siguientes características y servicios no están disponibles en Linux en el momento de la versión de disponibilidad general. La compatibilidad con estas características se habilitará cada vez más con el tiempo.

| Área | Característica o servicio no admitido |
|-----|-----|
| **Motor de base de datos** | Replicación transaccional |
| &nbsp; | Replicación de mezcla |
| &nbsp; | Captura de datos modificados (vea Agente SQL Server) |
| &nbsp; | Stretch DB |
| &nbsp; | PolyBase |
| &nbsp; | Consulta distribuida con conexiones de terceros |
| &nbsp; | Servidores vinculados a orígenes de datos distintos de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  |
| &nbsp; | Procedimientos almacenados extendidos del sistema (XP_CMDSHELL, etc.) |
| &nbsp; | Filetable, FILESTREAM |
| &nbsp; | Ensamblados CLR con el conjunto de permisos EXTERNAL_ACCESS o Unsafe |
| &nbsp; | Buffer Pool Extension |
| **Agente SQL Server** |  Subsistemas CmdExec, PowerShell, lector de colas, SSIS, SSAS, SSRS |
| &nbsp; | Alertas |
| &nbsp; | Agente de registro del LOG |
| &nbsp; | Captura de datos modificados (CDC) |
| &nbsp; | Copia de seguridad administrada |
| **Alta disponibilidad** | Creación de reflejo de base de datos  |
| **Seguridad** | Administración extensible de claves |
| &nbsp; | Autenticación de AD para servidores vinculados | 
| &nbsp; | Autenticación de AD para grupos de disponibilidad (AG) | 
| &nbsp; | herramientas de AD de terceros (Centrify, Vintela, Powerbroker) | 
| **Servicios** | SQL Server Browser |
| &nbsp; | SQL Server R Services |
| &nbsp; | StreamInsight |
| &nbsp; | Analysis Services |
| &nbsp; | Reporting Services |
| &nbsp; | Data Quality Services |
| &nbsp; | Master Data Services |
| &nbsp; | Coordinador de transacciones distribuidas (DTC) |

## <a name="known-issues"></a>Problemas conocidos

En las secciones siguientes se describen los problemas conocidos de la versión de disponibilidad general [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] (GA) de en Linux.

#### <a name="general"></a>General

- La longitud del nombre de host [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] donde está instalado debe ser de 15 caracteres como máximo. 

    - **Solución**: Cambie el nombre de/etc/hostname a una longitud de 15 caracteres o menos.

- Establecer manualmente la hora del sistema hacia atrás en el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiempo hará que deje de actualizar la hora [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]interna del sistema en.

    - **Solución**: Reinicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Solo se admiten instalaciones de instancia única.

    - **Solución**: Si desea tener más de una instancia en un host determinado, considere la posibilidad de usar máquinas virtuales o contenedores de Docker. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Configuration Manager no se puede [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conectar a en Linux.

- El idioma predeterminado del inicio de sesión de **SA** es el inglés.

    - **Solución**: Cambie el idioma del inicio de sesión **SA** por la instrucción **ALTER login** .

#### <a name="databases"></a>Bases de datos

- No se puede migrar la base de datos maestra con la utilidad MSSQL-conf. Otras bases de datos del sistema se pueden migrar con MSSQL-conf.

- Al restaurar una base de datos de la que se realizó [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] una copia de seguridad en Windows, debe utilizar la cláusula **with Move** en la instrucción Transact-SQL.

- Las transacciones distribuidas que requieren el servicio Microsoft Coordinador de transacciones distribuidas no se [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admiten en que se ejecutan en Linux. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] los servidores vinculados se admiten a menos que impliquen el DTC. Para obtener más información, consulte [las transacciones distribuidas que requieren el servicio Microsoft Coordinador de transacciones distribuidas no se admiten en SQL Server que se ejecutan en Linux](https://blogs.msdn.microsoft.com/bobsql/2017/12/11/sql-server-linux-distributed-transactions-requiring-the-microsoft-distributed-transaction-coordinator-service-are-not-supported-on-sql-server-running-on-linux-sql-server-to-sql-server-distributed-tr/).

- Ciertos algoritmos (conjuntos de cifrado) para la seguridad de la capa de transporte (TLS [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ) no funcionan correctamente con en Linux. Esto produce errores de conexión al intentar conectarse a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], así como problemas al establecer conexiones entre las réplicas de grupos de alta disponibilidad.

   - **Solución**: Modifique el script de configuración **MSSQL. conf** de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux para deshabilitar los conjuntos de cifrado problemáticos; para ello, haga lo siguiente:

      1. Agregue lo siguiente a/var/opt/MSSQL/MSSQL.conf.

      ```
      [network]
      tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
      ```

         >[!NOTE]
         >In the preceding code, `!` negates the expression. This tells OpenSSL to not use the following cipher suite.  

      1. Reinicie [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con el siguiente comando.

      ```bash
      sudo systemctl restart mssql-server
      ```

- [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]las bases de datos de Windows que usan OLTP en memoria no se pueden restaurar [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] en Linux. Para restaurar una [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] base de datos que utiliza OLTP en memoria, primero actualice las bases de datos [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] a [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] o en Windows antes de moverlas a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux mediante backup/restore o detach/Attach.

- En este momento no se admite la **Administración de operaciones masivas** de permisos de usuario en Linux.

#### <a name="networking"></a>Redes

Es posible que las características que implican conexiones TCP salientes desde el proceso Sqlservr, como servidores vinculados o grupos de disponibilidad, no funcionen si se cumplen las condiciones siguientes:

1. El servidor de destino se especifica como un nombre de host y no como una dirección IP.

1. La instancia de de origen tiene IPv6 deshabilitado en el kernel. Para comprobar si el sistema tiene IPv6 habilitado en el kernel, deben cumplirse todas las pruebas siguientes:

   - `cat /proc/cmdline`imprimirá el cmdline de arranque del kernel actual. La salida no debe contener `ipv6.disable=1`.
   - El directorio/proc/sys/net/IPv6/debe existir.
   - Un programa de C que `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` llama a debe ser correcto: syscall debe devolver un FD! =-1 y no producir un error con EAFNOSUPPORT.

El error exacto depende de la característica. En el caso de los servidores vinculados, esto se manifiesta como un error de tiempo de espera de inicio de sesión. En el caso de los `ALTER AVAILABILITY GROUP JOIN` grupos de disponibilidad, el DDL de la secundaria producirá un error después de 5 minutos con un error de tiempo de espera de configuración de descarga.

Para solucionar este problema, realice una de las acciones siguientes:

1. Use direcciones IP en lugar de nombres de host para especificar el destino de la conexión TCP.

1. Habilite IPv6 en el kernel quitando `ipv6.disable=1` de la cmdline de arranque. La manera de hacerlo depende de la distribución de Linux y del cargador de arranque, como grub. Si desea que IPv6 esté deshabilitado, todavía puede deshabilitarlo `net.ipv6.conf.all.disable_ipv6 = 1` estableciendo en la `sysctl` configuración (por ejemplo `/etc/sysctl.conf`,). Esto impedirá que el adaptador de red del sistema obtenga una dirección IPv6, pero permite que las características de sqlservr funcionen.

#### <a name="network-file-system-nfs"></a>Network File System (NFS)
Si usa recursos compartidos remotos de **Network File System (NFS)** en producción, tenga en cuenta los siguientes requisitos de compatibilidad:

- Use la versión **4,2 de NFS o posterior**. Las versiones anteriores de NFS no admiten las características requeridas, como fallocate y la creación de archivos dispersos, comunes a los sistemas de archivos modernos.
- Busque solo los directorios de **/var/opt/MSSQL** en el montaje de NFS. No se admiten otros archivos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como los archivos binarios del sistema.
- Asegúrese de que los clientes NFS usan la opción ' NOLOCK ' al montar el recurso compartido remoto.

#### <a name="localization"></a>Localización

- Si su configuración regional no es inglés (en_US) durante la instalación, debe usar la codificación UTF-8 en la sesión o el terminal de Bash. Si usa la codificación ASCII, es posible que vea un error similar al siguiente:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Si no puede usar la codificación UTF-8, ejecute el programa de instalación mediante la variable de entorno MSSQL_LCID para especificar el idioma que prefiera.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Al ejecutar el programa de instalación de MSSQL-conf y realizar una instalación que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]no esté en Inglés de, se muestran caracteres extendidos incorrectos después del texto localizado "configurando SQL Server...". O bien, en el caso de las instalaciones no basadas en latín, la oración podría faltar por completo. La oración que falta debe mostrar la siguiente cadena localizada: "El PID de licencia se procesó correctamente. La nueva edición es [\<nombre\> de la edición] ". Esta cadena solo se muestra con fines informativos y la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] siguiente actualización acumulativa lo solucionará en todos los idiomas. Esto no afecta a la instalación correcta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de ninguna manera. 

#### <a name="full-text-search"></a>Búsqueda de texto completo

- No todos los filtros están disponibles en esta versión, incluidos los filtros para documentos de Office. Para obtener una lista de filtros compatibles, consulte [SQL Server instalación de la búsqueda de texto completo en Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a id="ssis"></a> SQL Server Integration Services (SSIS)

- El paquete **MSSQL-Server-is** no es compatible con SuSE en esta versión. Actualmente se admite en Ubuntu y en Red Hat Enterprise Linux (RHEL).

- Con [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en Linux CTP 2,1 refresh y versiones posteriores [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , los paquetes pueden usar conexiones ODBC en Linux. Esta funcionalidad se ha probado con los [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] controladores ODBC de MySQL, pero también se espera que funcione con cualquier controlador ODBC de Unicode que respete la especificación de ODBC. En tiempo de diseño, puede proporcionar un DSN o una cadena de conexión para conectarse a los datos ODBC; también puede usar la autenticación de Windows. Para obtener más información, consulte la [entrada de blog que anuncia la compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- No se admiten las siguientes características en esta versión al ejecutar paquetes SSIS en Linux:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]Base de datos de catálogo
  - Ejecución de paquetes programada por el Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Captura de datos modificados (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]Escalabilidad horizontal
  - Feature Pack de Azure para SSIS
  - Compatibilidad con Hadoop y HDFS
  - Microsoft Connector for SAP BW

Para obtener una lista de componentes de SSIS integrados que no se admiten actualmente o que son compatibles con las limitaciones, consulte [limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md#components).

Para obtener más información sobre SSIS en Linux, consulte los siguientes artículos:
-   [Entrada de blog que anuncia la compatibilidad de SSIS con Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalación de SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)

#### <a id="ssms"></a> SQL Server Management Studio (SSMS)

Las siguientes limitaciones se aplican a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] en Windows conectado a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en Linux.

- No se admiten los planes de mantenimiento.

- No se admiten el almacén de administración de datos ( [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] MDW) y el recopilador de datos en. 

- [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]Los componentes de interfaz de usuario que tienen opciones de registro de eventos de Windows o de autenticación de Windows no funcionan con Linux. Todavía puede usar estas características con otras opciones, como inicios de sesión de SQL. 

- No se puede modificar el número de archivos de registro que se van a conservar.

## <a name="next-steps"></a>Pasos siguientes

Para empezar, consulte las siguientes guías de inicio rápido:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalación en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecución en Docker](quickstart-install-connect-ubuntu.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Ejecución y conexión: nube](quickstart-install-connect-clouds.md)

Para obtener respuestas a las preguntas más frecuentes, consulte las [preguntas más frecuentes sobre SQL Server en Linux](sql-server-linux-faq.md).
