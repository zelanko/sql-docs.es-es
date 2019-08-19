---
title: Notas de la versión de SQL Server 2019 | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 40040948b56190a3ce94d9484e09a3386548bd31
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028855"
---
# <a name="sql-server-2019-preview-release-notes"></a>Notas de la versión preliminar de SQL Server 2019
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describen las limitaciones y los problemas conocidos de las versiones de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Community Technology Preview (CTP). Para obtener información relacionada, consulte estos artículos:
- [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)

## <a name="ctp-32"></a>CTP 3.2

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2 es la versión pública más reciente de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2 está disponible únicamente como edición de evaluación. No hay más ediciones disponibles.

Encontrará información completa sobre la compatibilidad y la administración de licencias de versiones de CTP en `license_Eval.rtf` con sus soportes de instalación.

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

## <a name="documentation"></a>Documentación

- **Problema e impacto en el cliente**: La documentación de SQL Server 2019 (15.x) es limitada, y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El contenido de los artículos específicos de SQL Server 2019 (15.x) se distinguirá con **Se aplica a**.

- **Problema e impacto en el cliente**: la documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se puede filtrar por versión. Use el control situado en la parte superior izquierda de cada página de documentación para filtrar según sus requisitos.

- **Problema e impacto en el cliente**: No hay ningún contenido sin conexión disponible para SQL Server 2019 (15.x).

## <a name="hardware-and-software-requirements"></a>Requisitos de hardware y software

- **Problema e impacto en el cliente**: Los requisitos de hardware y software aún están en revisión y no son definitivos para la versión del producto.

  - **Hardware**
    - [Windows: requisitos de procesador, memoria y sistema operativo](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux: requisitos del sistema](../linux/sql-server-linux-setup.md#system)
  - **Software**
    - Windows Server 2016 o una versión posterior. Para ver más requisitos, consulte [Requisitos para instalar SQL Server](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2. Disponible en el [Centro de descarga](https://www.microsoft.com/download/details.aspx?id=53344).
    - En cuanto a Linux, consulte [Linux: Plataformas compatibles](../linux/sql-server-linux-setup.md#supportedplatforms)

## <a name = "release-notes"></a>Características que se excluyen del soporte técnico

- **Problema e impacto en el cliente:** [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] no ofrece soporte técnico para los componentes, las características y los escenarios siguientes:
  - SQL Server Analysis Services
  - SQL Server Reporting Services
  - Grupos de disponibilidad AlwaysOn en Kubernetes
  - Recuperación acelerada de bases de datos.

- **Solución**: Ninguno. La exclusión se aplica a todos los clientes, incluidos los participantes en el programa de adopción temprana de SQL.

- **Se aplica a**: todas las versiones de CTP

## <a name="updated-compiler"></a>Compilador actualizado

- **Problema e impacto en el cliente**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] incorpora un compilador actualizado. CTP 2.1 tenía un problema conocido por el que los resultados de un número de punto flotante y otros escenarios de conversión podían devolver un valor distinto al devuelto en versiones anteriores debido al compilador actualizado. CTP 2.2 incluye recursos para asegurarse de que los escenarios afectados devuelvan los mismos resultados que las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No se ha detectado ninguna otra incidencia en CTP 3.2. Notifique cualquier anomalía en los resultados en comparación con [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] al equipo de [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ](https://aka.ms/sqlfeedback) inmediatamente.

- **Solución**: N/D

- **Se aplica a**: todas las versiones de CTP

## <a name="installation-wizard-may-wait-between-eula-pages"></a>El asistente para la instalación puede esperar entre las páginas de CLUF

- **Problema e impacto en el cliente**: durante la instalación con el asistente para la instalación, el proceso puede esperar una cantidad excesiva de tiempo entre el contrato de licencia del usuario final (CLUF) para R Services y el CLUF para Python.

- **Solución**: espere a que el asistente para la instalación termine. El tiempo de espera puede superar los 30 minutos.

- **Se aplica a**: SQL Server 2019 CTP 3.0

## <a name="utf-8-collations"></a>Intercalaciones UTF-8

- **Problema e impacto en el cliente**: No se pueden usar las intercalaciones habilitadas para UTF-8 con algunas otras características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. UTF-8 no es compatible si se utilizan las siguientes características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:

  - OLTP en memoria
  - Tabla externa para PolyBase
  - Always Encrypted

  > [!Note]
  > Actualmente, no hay ninguna compatibilidad de interfaz de usuario para elegir intercalaciones habilitadas para UTF-8 en Azure Data Studio o SQL Server Data Tools (SSDT). La versión 18, la más reciente de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS), permite elegir las intercalaciones habilitadas para UTF-8 en la interfaz de usuario.
 
- **Solución**: No hay ninguna solución alternativa para [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP.

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2, CTP 3.1, CTP 3.0, CTP 2.5, CTP 2.4, CTP 2.3, CTP 2.2, CTP 2.1, CTP 2.0.

## <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclaves seguros

- **Problema e impacto en el cliente**: Los cálculos completos son optimizaciones de rendimiento pendientes y mejoras en el control de errores, y actualmente están deshabilitados de forma predeterminada.

- **Solución**: Para habilitar los cálculos completos, ejecute `DBCC traceon(127,-1)`. Para obtener más información, consulte [Habilitar cálculos completos](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.2, CTP 3.1

## <a name="sql-server-configuration-manager-may-not-start"></a>Administrador de configuración de SQL Server puede no iniciarse

- **Problema e impacto en el cliente**: Administrador de configuración de SQL Server (SSCM) no se inicia en un equipo sin VCRuntime 140. Al iniciar SSCM, el usuario puede ver el cuadro de diálogo siguiente: 

  `
  MMC could not create the snap-in. The snap-in might not have been installed correctly.
  `

- **Solución**:  Instale la versión más reciente de VC Runtime 2013 (x86):

  - [Verbose](https://support.microsoft.com/help/2977003/the-latest-supported-visual-c-downloads)
  - [Direct](https://support.microsoft.com/en-us/help/4032938/update-for-visual-c-2013-redistributable-package)

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 3.1, CTP 3.0, CTP 2.5.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
