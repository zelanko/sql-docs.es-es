---
title: Notas de la versión preliminar de SQL Server 2019 en Linux
description: En este artículo se incluyen las notas de la versión y las características admitidas de la versión preliminar de SQL Server 2019 que se ejecuta en Linux. Se incluyen las notas de la versión más reciente y de varias versiones anteriores.
author: VanMSFT
ms.author: vanto
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 296581ab8052a7eab384721664fc10d675bb2d06
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68476031"
---
# <a name="release-notes-for-sql-server-2019-preview-on-linux"></a>Notas de la versión preliminar de SQL Server 2019 en Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

Las siguientes notas de la versión se aplican a la versión preliminar de SQL Server 2019 que se ejecuta en Linux. Este artículo se divide en secciones para cada versión. Cada versión tiene un vínculo a un artículo de asistencia en el que se describen los cambios de la CU, así como vínculos a las descargas de los paquetes de Linux.

> [!TIP]
> Para obtener información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).

## <a name="supported-platforms"></a>Plataformas compatibles

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5 o 7.6 Server | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de Docker 1.8 y versiones posteriores en Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obtener más información, consulte los [requisitos del sistema](sql-server-linux-setup.md#system) para SQL Server en Linux. Para obtener la directiva de soporte técnico más reciente para SQL Server 2017, consulte la [Directiva de soporte técnico de Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Herramientas

La mayoría de las herramientas cliente existentes que tienen SQL Server como destino pueden dirigirse sin problemas a SQL Server en ejecución en Linux. Algunas herramientas pueden tener un requisito de versión específico para funcionar bien con Linux. Para obtener una lista completa de las herramientas de SQL Server, vea [Herramientas y utilidades de SQL para SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Historial de versiones

En la tabla siguiente se muestra el historial de las versiones CTP de la versión preliminar de SQL Server 2019.

| Versión               | Versión       | Fecha de la versión |
|-----------------------|---------------|--------------|
| [CTP 3.2](#CTP32)     | 15.0.1800.32  | 2019-7-24    |
| [CTP 3.1](#CTP31)     | 15.0.1700.37  | 2019-6-26    |
| [CTP 3.0](#CTP30)     | 15.0.1600.8   | 2019-5-22    |
| [CTP 2.5](#CTP25)     | 15.0.1500.28  | 2019-4-24    |
| [CTP 2.4](#CTP24)     | 15.0.1400.75  | 2019-3-27    |
| [CTP 2.3](#CTP23)     | 15.0.1300.359 | 2019-3-01    |
| [CTP 2.2](#CTP22)     | 15.0.1200.24  | 2018-12-11   |
| [CTP 2.1](#CTP21)     | 15.0.1100.94  | 2018-11-06   |
| [CTP 2.0](#CTP20)     | 15.0.1000.34  | 2018-09-24   |

## <a id="cuinstall"></a> Procedimiento para instalar las actualizaciones

Si ha configurado el repositorio de versión preliminar (**mssql-server-preview**), obtendrá los paquetes de CTP de SQL Server más recientes al realizar nuevas instalaciones. Si necesita imágenes de contenedor de Docker, consulte las imágenes oficiales de [Microsoft SQL Server en Linux para el motor de Docker](https://hub.docker.com/r/microsoft/mssql-server/). Para obtener más información sobre la configuración del repositorio, consulte [Configurar repositorios de SQL Server en Linux](sql-server-linux-change-repo.md).

Si va a actualizar paquetes de SQL Server existentes, ejecute el comando de actualización adecuado para cada paquete a fin de obtener la CU más reciente. Para obtener instrucciones de actualización específicas para cada paquete, vea las siguientes guías de instalación:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar el paquete de búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Instalar la compatibilidad con R y Python de la versión preliminar de SQL Server 2019 Machine Learning Services en Linux](sql-server-linux-setup-machine-learning.md)
- [Instalación del paquete de PolyBase](../relational-databases/polybase/polybase-linux-setup.md)
- [Habilitación del Agente SQL Server](sql-server-linux-setup-sql-agent.md)

## <a id="CTP32"></a> CTP 3.2 (julio de 2019)

En las secciones siguientes se proporcionan las ubicaciones de los paquetes y problemas conocidos de la versión CTP 3.2. Para obtener más información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1800.32-1 | [Paquete de RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| Paquete de RPM de SLES | 15.0.1800.32-1 | [Paquete de RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1800.32-1.x86_64.rpm)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1800.32-1.x86_64.rpm)|
| Paquete de Ubuntu 16.04 Debian | 15.0.1800.32-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1800.32-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1800.32-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1800.32-1_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1800.32-1_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1800.32-1_amd64.deb)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1800.32-1_amd64.deb)|

## <a id="CTP31"></a> CTP 3.1 (junio de 2019)

En las secciones siguientes se proporcionan las ubicaciones de los paquetes y problemas conocidos de la versión CTP 3.1. Para obtener más información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1700.37-2 | [Paquete de RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Paquete de RPM de SLES | 15.0.1700.37-2 | [Paquete de RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1700.37-2.x86_64.rpm)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1700.37-2.x86_64.rpm)|
| Paquete de Ubuntu 16.04 Debian | 15.0.1700.37-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1700.37-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1700.37-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1700.37-2_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1700.37-2_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1700.37-2_amd64.deb)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1700.37-2_amd64.deb)|

## <a id="CTP30"></a> CTP 3.0 (mayo de 2019)

En las secciones siguientes se proporcionan las ubicaciones de los paquetes y problemas conocidos de la versión CTP 3.0. Para obtener más información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1600.8-1 | [Paquete de RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Paquete de RPM de SLES | 15.0.1600.8-1 | [Paquete de RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Paquete de Ubuntu 16.04 Debian | 15.0.1600.8-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1600.8-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1600.8-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1600.8-1_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1600.8-1_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1600.8-1_amd64.deb)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1600.8-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Microsoft DTC (Coordinador de transacciones distribuidas)

Actualmente, MSDTC requiere que las transacciones no se autentiquen. Por ejemplo, si usa un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usa una aplicación cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, se requiere MSDTC en el cliente o servidor de Windows para usar la opción "No se requiere autenticación".

## <a id="CTP25"></a> CTP 2.5 (abril de 2019)

En las secciones siguientes se proporcionan las ubicaciones de los paquetes y problemas conocidos de la versión CTP 2.5. Para obtener más información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1500.28-1 | [Paquete de RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Paquete de RPM de SLES | 15.0.1500.28-1 | [Paquete de RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Paquete de Ubuntu 16.04 Debian | 15.0.1500.28-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1500.28-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1500.28-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1500.28-1_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1500.28-1_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1500.28-1_amd64.deb)</br>[Paquete de RPM de PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1500.28-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Microsoft DTC (Coordinador de transacciones distribuidas)

Actualmente, MSDTC requiere que las transacciones no se autentiquen. Por ejemplo, si usa un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usa una aplicación cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, se requiere MSDTC en el cliente o servidor de Windows para usar la opción "No se requiere autenticación".

## <a id="CTP24"></a> CTP 2.4 (marzo de 2019)

En las secciones siguientes se proporcionan las ubicaciones de los paquetes y problemas conocidos de la versión CTP 2.4. Para obtener más información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1400.75-2 | [Paquete de RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Paquete de RPM de SLES | 15.0.1400.75-2 | [Paquete de RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Paquete de Ubuntu 16.04 Debian | 15.0.1400.75-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1400.75-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1400.75-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1400.75-2_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1400.75-2_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1400.75-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Microsoft DTC (Coordinador de transacciones distribuidas)

Actualmente, MSDTC requiere que las transacciones no se autentiquen. Por ejemplo, si usa un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usa una aplicación cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, se requiere MSDTC en el cliente o servidor de Windows para usar la opción "No se requiere autenticación".

## <a id="CTP23"></a> CTP 2.3 (febrero de 2019)

En las secciones siguientes se proporcionan las ubicaciones de los paquetes y problemas conocidos de la versión CTP 2.3. Para obtener más información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1300.359-1 | [Paquete de RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Paquete de RPM de SLES | 15.0.1300.359-1 | [Paquete de RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Paquete de Ubuntu 16.04 Debian | 15.0.1300.359-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1300.359-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1300.359-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1300.359-1_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1300.359-1_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1300.359-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Microsoft DTC (Coordinador de transacciones distribuidas)

Actualmente, MSDTC requiere que las transacciones no se autentiquen. Por ejemplo, si usa un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usa una aplicación cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, se requiere MSDTC en el cliente o servidor de Windows para usar la opción "No se requiere autenticación".

## <a id="CTP22"></a> CTP 2.2 (diciembre de 2018)

En las secciones siguientes se proporcionan las ubicaciones de los paquetes y problemas conocidos de la versión CTP 2.2. Para obtener más información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1200.24-2 | [Paquete de RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Paquete de RPM de SLES | 15.0.1200.24-2 | [Paquete de RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Paquete de Ubuntu 16.04 Debian | 15.0.1200.24-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1200.24-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1200.24-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1200.24-2_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1200.24-2_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1200.24-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Microsoft DTC (Coordinador de transacciones distribuidas)

Actualmente, MSDTC requiere que las transacciones no se autentiquen. Por ejemplo, si usa un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usa una aplicación cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, se requiere MSDTC en el cliente o servidor de Windows para usar la opción "No se requiere autenticación".

## <a id="CTP21"></a> CTP 2.1 (noviembre de 2018)

En las secciones siguientes se proporcionan las ubicaciones de los paquetes y problemas conocidos de la versión CTP 2.1. Para obtener más información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1100.94-1 | [Paquete de RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Paquete de RPM de SLES | 15.0.1100.94-1 | [Paquete de RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Paquete de Ubuntu 16.04 Debian | 15.0.1100.94-1 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft DTC (Coordinador de transacciones distribuidas)

Actualmente, MSDTC requiere que las transacciones no se autentiquen. Por ejemplo, si usa un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usa una aplicación cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, se requiere MSDTC en el cliente o servidor de Windows para usar la opción "No se requiere autenticación".

## <a id="CTP20"></a> CTP 2.0 (septiembre de 2018)

En las secciones siguientes se proporcionan las ubicaciones de los paquetes y problemas conocidos de la versión CTP 2.0. Para obtener más información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

En el caso de las instalaciones de paquetes manuales o sin conexión, puede descargar los paquetes RPM y Debian con la información de la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1000.34-2 | [Paquete de RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Paquete de RPM de SLES | 15.0.1000.34-2 | [Paquete de RPM del motor mssql-server](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de alta disponibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de la búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Paquete de Ubuntu 16.04 Debian | 15.0.1000.34-2 | [Paquete de Debian del motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[Paquete de Debian de la búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a name="microsoft-distributed-transaction-coordinator"></a>Microsoft DTC (Coordinador de transacciones distribuidas)

Actualmente, MSDTC requiere que las transacciones no se autentiquen. Por ejemplo, si usa un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usa una aplicación cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, se requiere MSDTC en el cliente o servidor de Windows para usar la opción "No se requiere autenticación".

## <a name="next-steps"></a>Pasos siguientes

Para empezar, consulte las siguientes guías de inicio rápido:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalación en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecución en Docker](quickstart-install-connect-ubuntu.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Ejecución y conexión: nube](quickstart-install-connect-clouds.md)

Para obtener respuesta a las preguntas más frecuentes, consulte las [Preguntas más frecuentes sobre SQL Server en Linux](sql-server-linux-faq.md).
