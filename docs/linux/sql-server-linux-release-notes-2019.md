---
title: Notas de versión preliminar de SQL Server 2019 en Linux | Microsoft Docs
description: En este artículo contiene las notas de la versión y las características admitidas para la versión preliminar de 2019 de SQL Server que se ejecutan en Linux. Notas de la versión se incluyen para la versión más reciente y varias versiones anteriores.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/22/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 8645fc41b518618194a62f24e3826b31a56596ad
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705266"
---
# <a name="release-notes-for-sql-server-2019-preview-on-linux"></a>Notas de la versión de vista previa de 2019 de SQL Server en Linux

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-linuxonly.md)]

Las notas siguientes se aplican a la versión preliminar de 2019 de SQL Server que se ejecutan en Linux. Este artículo está dividido en secciones para cada versión. Cada versión tiene un vínculo a un artículo de soporte técnico que describe la CU de cambios, así como vínculos a la descargas de paquetes de Linux.

> [!TIP]
> Para obtener información sobre las nuevas características de Linux en SQL Server 2019, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).

## <a name="supported-platforms"></a>Plataformas compatibles

| Plataforma | Sistema de archivos | Guía de instalación |
|-----|-----|-----|
| Servidor de Red Hat Enterprise Linux 7.3, 7.4, 7.5 o 7.6 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-suse.md) |
| Ubuntu 16.04LTS | XFS o EXT4 | [Guía de instalación](quickstart-install-connect-ubuntu.md) | 
| Motor de docker 1.8 y versiones posteriores on Windows, Mac o Linux | N/D | [Guía de instalación](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obtener más información, revise el [requisitos del sistema](sql-server-linux-setup.md#system) para SQL Server en Linux. Para la directiva de soporte técnico más reciente para SQL Server 2017, consulte el [directiva de soporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Herramientas

La mayoría herramientas de cliente existentes que tienen como destino de SQL Server pueden tener como destino SQL Server que se ejecutan en Linux sin problemas. Algunas herramientas pueden tener un requisito de versión específica para funcionar bien con Linux. Para obtener una lista completa de herramientas de SQL Server, vea [SQL herramientas y utilidades de SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Historial de versiones

La tabla siguiente muestra el historial de versión de vista previa de SQL Server 2019 que versiones de CTP.

| Versión               | Versión       | Fecha de la versión |
|-----------------------|---------------|--------------|
| [CTP 3.0](#CTP30)     | 15.0.1600.8  | 2019-5-22    |
| [CTP 2.5](#CTP25)     | 15.0.1500.28  | 2019-4-24    |
| [CTP 2.4](#CTP24)     | 15.0.1400.75  | 2019-3-27    |
| [CTP 2.3](#CTP23)     | 15.0.1300.359 | 2019-3-01    |
| [CTP 2.2](#CTP22)     | 15.0.1200.24  | 2018-12-11   |
| [CTP 2.1](#CTP21)     | 15.0.1100.94  | 2018-11-06   |
| [CTP 2.0](#CTP20)     | 15.0.1000.34  | 2018-09-24   |

## <a id="cuinstall"></a> Cómo instalar actualizaciones

Si ha configurado el repositorio de vista previa (**mssql-server-vista previa**), obtendrá los paquetes más recientes de la CTP de SQL Server al realizar nuevas instalaciones. Si se requieren imágenes de contenedor de Docker, consulte las imágenes oficiales de [Microsoft SQL Server en Linux para el motor de Docker](https://hub.docker.com/r/microsoft/mssql-server/). Para obtener más información acerca de la configuración del repositorio, consulte [configurar repositorios para SQL Server en Linux](sql-server-linux-change-repo.md).

Si va a actualizar los paquetes existentes de SQL Server, ejecute el comando de actualización adecuada para cada paquete obtener la CU más reciente. Para obtener instrucciones de actualización específica para cada paquete, consulte las guías de instalación siguientes:

- [Instalar el paquete de SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar el paquete de búsqueda de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Instalar la versión preliminar de SQL Server 2019 R de Machine Learning Services y compatibilidad con Python en Linux](sql-server-linux-setup-machine-learning.md)
- [Habilitar el Agente SQL Server](sql-server-linux-setup-sql-agent.md)
- [Instalación de PolyBase Linux](../relational-databases/polybase/polybase-linux-setup.md)

## <a id="CTP30"></a> CTP 3.0 (mayo de 2019)

Las secciones siguientes proporcionan ubicaciones de los paquetes y problemas conocidos de la CTP 3.0 liberar. Para obtener más información acerca de las nuevas características para Linux en SQL Server 2019, vea el [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1600.8-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[Paquete RPM de PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Paquete RPM SLES | 15.0.1600.8-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1600.8-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1600.8-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1600.8-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1600.8-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1600.8-1.x86_64.rpm)</br>[Paquete RPM de PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1600.8-1.x86_64.rpm)|
| Paquete de Debian Ubuntu 16.04 | 15.0.1600.8-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1600.8-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1600.8-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1600.8-1_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1600.8-1_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1600.8-1_amd64.deb)</br>[Paquete RPM de PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1600.8-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Coordinador de transacciones distribuidas de Microsoft

Actualmente, MSDTC requiere que las transacciones no autenticados. Por ejemplo, si está usando un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usar una aplicación de cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, a continuación, MSDTC en Windows server o cliente es necesario usar la opción "No Se requiere autenticación".

## <a id="CTP25"></a> CTP 2.5 (ABR de 2019)

Las secciones siguientes proporcionan ubicaciones de los paquetes y problemas conocidos para la 2.5 de CTP de versión. Para obtener más información acerca de las nuevas características para Linux en SQL Server 2019, vea el [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1500.28-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[Paquete RPM de PolyBase](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Paquete RPM SLES | 15.0.1500.28-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1500.28-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1500.28-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1500.28-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1500.28-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1500.28-1.x86_64.rpm)</br>[Paquete RPM de PolyBase](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-polybase-15.0.1500.28-1.x86_64.rpm)|
| Paquete de Debian Ubuntu 16.04 | 15.0.1500.28-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1500.28-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1500.28-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1500.28-1_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1500.28-1_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1500.28-1_amd64.deb)</br>[Paquete RPM de PolyBase](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-polybase/mssql-server-polybase_15.0.1500.28-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Coordinador de transacciones distribuidas de Microsoft

Actualmente, MSDTC requiere que las transacciones no autenticados. Por ejemplo, si está usando un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usar una aplicación de cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, a continuación, MSDTC en Windows server o cliente es necesario usar la opción "No Se requiere autenticación".

## <a id="CTP24"></a> CTP 2.4 (marzo de 2019)

Las secciones siguientes proporcionan las ubicaciones de paquete y versión de los problemas conocidos de la CTP 2.4. Para obtener más información acerca de las nuevas características para Linux en SQL Server 2019, vea el [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1400.75-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Paquete RPM SLES | 15.0.1400.75-2 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1400.75-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1400.75-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1400.75-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1400.75-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1400.75-2.x86_64.rpm)|
| Paquete de Debian Ubuntu 16.04 | 15.0.1400.75-2 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1400.75-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1400.75-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1400.75-2_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1400.75-2_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1400.75-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Coordinador de transacciones distribuidas de Microsoft

Actualmente, MSDTC requiere que las transacciones no autenticados. Por ejemplo, si está usando un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usar una aplicación de cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, a continuación, MSDTC en Windows server o cliente es necesario usar la opción "No Se requiere autenticación".

## <a id="CTP23"></a> CTP 2.3 (febrero de 2019)

Las secciones siguientes proporcionan las ubicaciones de paquete y versión de los problemas conocidos de la CTP 2.3. Para obtener más información acerca de las nuevas características para Linux en SQL Server 2019, vea el [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1300.359-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Paquete RPM SLES | 15.0.1300.359-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1300.359-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1300.359-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1300.359-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1300.359-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1300.359-1.x86_64.rpm)|
| Paquete de Debian Ubuntu 16.04 | 15.0.1300.359-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1300.359-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1300.359-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1300.359-1_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1300.359-1_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1300.359-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Coordinador de transacciones distribuidas de Microsoft

Actualmente, MSDTC requiere que las transacciones no autenticados. Por ejemplo, si está usando un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usar una aplicación de cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, a continuación, MSDTC en Windows server o cliente es necesario usar la opción "No Se requiere autenticación".

## <a id="CTP22"></a> CTP 2.2 (diciembre de 2018)

Las secciones siguientes proporcionan ubicaciones de los paquetes y problemas conocidos de la CTP 2.2 de versión. Para obtener más información acerca de las nuevas características para Linux en SQL Server 2019, vea el [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1200.24-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Paquete RPM SLES | 15.0.1200.24-2 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1200.24-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1200.24-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1200.24-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1200.24-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1200.24-2.x86_64.rpm)|
| Paquete de Debian Ubuntu 16.04 | 15.0.1200.24-2 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1200.24-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1200.24-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1200.24-2_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1200.24-2_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1200.24-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a id="msdtc"></a> Coordinador de transacciones distribuidas de Microsoft

Actualmente, MSDTC requiere que las transacciones no autenticados. Por ejemplo, si está usando un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usar una aplicación de cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, a continuación, MSDTC en Windows server o cliente es necesario usar la opción "No Se requiere autenticación".

## <a id="CTP21"></a> CTP 2.1 (noviembre de 2018)

Las secciones siguientes proporcionan las ubicaciones de paquete y versión de los problemas conocidos de la CTP 2.1. Para obtener más información acerca de las nuevas características para Linux en SQL Server 2019, vea el [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1100.94-1 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Paquete RPM SLES | 15.0.1100.94-1 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1100.94-1.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1100.94-1.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1100.94-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1100.94-1.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1100.94-1.x86_64.rpm)|
| Paquete de Debian Ubuntu 16.04 | 15.0.1100.94-1 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1100.94-1_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1100.94-1_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1100.94-1_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1100.94-1_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1100.94-1_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a name="microsoft-distributed-transaction-coordinator"></a>Coordinador de transacciones distribuidas de Microsoft

Actualmente, MSDTC requiere que las transacciones no autenticados. Por ejemplo, si está usando un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usar una aplicación de cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, a continuación, MSDTC en Windows server o cliente es necesario usar la opción "No Se requiere autenticación".

## <a id="CTP20"></a> En CTP 2.0 (septiembre de 2018)

Las secciones siguientes proporcionan ubicaciones de los paquetes y problemas conocidos de la versión 2.0 de CTP de versión. Para obtener más información acerca de las nuevas características para Linux en SQL Server 2019, vea el [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

### <a name="package-details"></a>Detalles del paquete

Para las instalaciones de paquete manual o sin conexión, puede descargar los paquetes RPM y Debian con la información en la tabla siguiente:

| Paquete | Versión del paquete | Descargas |
|-----|-----|-----|
| Paquete de Red Hat RPM | 15.0.1000.34-2 | [Paquete RPM del motor](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/rhel/7/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Paquete RPM SLES | 15.0.1000.34-2 | [paquete de MSSQL-server motor RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-15.0.1000.34-2.x86_64.rpm)</br>[Paquete alta disponibilidad RPM](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-ha-15.0.1000.34-2.x86_64.rpm)</br>[Paquete de RPM de búsqueda de texto completo](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-fts-15.0.1000.34-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-15.0.1000.34-2.x86_64.rpm)</br>[Paquete RPM de extensibilidad de Java](https://packages.microsoft.com/sles/12/mssql-server-preview/mssql-server-extensibility-java-15.0.1000.34-2.x86_64.rpm)|
| Paquete de Debian Ubuntu 16.04 | 15.0.1000.34-2 | [Paquete de Debian motor](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server/mssql-server_15.0.1000.34-2_amd64.deb)</br>[Paquete de Debian de alta disponibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-ha/mssql-server-ha_15.0.1000.34-2_amd64.deb)</br>[Paquete de Debian de búsqueda de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-fts/mssql-server-fts_15.0.1000.34-2_amd64.deb)</br>[Paquete de Debian de extensibilidad](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility/mssql-server-extensibility_15.0.1000.34-2_amd64.deb)</br>[Paquete de Debian de extensibilidad de Java](https://packages.microsoft.com/ubuntu/16.04/mssql-server-preview/pool/main/m/mssql-server-extensibility-java/mssql-server-extensibility-java_15.0.1000.34-2_amd64.deb)|

### <a name="known-issues"></a>Problemas conocidos

#### <a name="microsoft-distributed-transaction-coordinator"></a>Coordinador de transacciones distribuidas de Microsoft

Actualmente, MSDTC requiere que las transacciones no autenticados. Por ejemplo, si está usando un servidor vinculado de SQL Server en Windows para SQL Server en Linux o usar una aplicación de cliente de Windows para iniciar una transacción distribuida en SQL Server en Linux, a continuación, MSDTC en Windows server o cliente es necesario usar la opción "No Se requiere autenticación".

## <a name="next-steps"></a>Pasos siguientes

Para empezar, vea los tutoriales siguientes:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalación en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-ubuntu.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Ejecución y conexión: nube](quickstart-install-connect-clouds.md)

Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](sql-server-linux-faq.md).
