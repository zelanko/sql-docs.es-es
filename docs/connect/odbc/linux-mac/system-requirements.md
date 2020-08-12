---
title: Requisitos del sistema (controlador ODBC para SQL Server)
description: Aquí se enumeran los requisitos del sistema para el controlador ODBC para SQL Server en los sistemas operativos Linux y macOS.
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01a5dd44d111fd72d76db244c8135d3bdde00ec8
ms.sourcegitcommit: cb620c77fe6bdefb975968837706750c31048d46
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2020
ms.locfileid: "86391760"
---
# <a name="system-requirements-linux-and-macos"></a>Requisitos del sistema (Linux y macOS)

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este tema se muestran los requisitos para utilizar [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y MacOS.

## <a name="sql-version-compatibility"></a>Compatibilidad con versiones de SQL

La compatibilidad con la versión de SQL de los controladores de Linux y macOS es la misma que la de los [controladores de Windows](../windows/system-requirements-installation-and-driver-files.md#sql-version-compatibility).

## <a name="operating-system-support"></a>Compatibilidad con sistema operativo

Las versiones 17, 13.1 y 13 de los controladores de Linux y macOS se admiten en la arquitectura x64 de los sistemas operativos siguientes:

|Sistema operativo compatible     |17.5|17.4|17.3|17.2|17.1|17.0|13.1|13|
|-------------------------------|----|----|----|----|----|----|----|--|
|Apple OS X 10.11 (El Capitan)  | |Y|Y|Y|Y|Y|Y|Y|
|Apple macOS 10.12 (Sierra)     | |Y|Y|Y|Y|Y|Y|Y|
|Apple macOS 10.13 (High Sierra)|Y|Y|Y|Y|Y|Y|Y|Y|
|Apple macOS 10.14 (Mojave)     |Y|Y|Y| | | | | |
|Apple macOS 10.15 (Catalina)   |Y| | | | | | | |
|Alpine Linux 3.11              |Y| | | | | | | |
|Debian Linux 8                 | |Y|Y|Y|Y|Y|Y|Y|
|Debian Linux 9                 |Y|Y|Y|Y|Y|Y|Y|Y|
|Debian Linux 10                |Y|Y| | | | | | |
|Oracle Linux 8                 |Y| | | | | | | |
|RedHat Enterprise Linux 6      |Y|Y|Y|Y|Y|Y|Y|Y|
|RedHat Enterprise Linux 7      |Y|Y|Y|Y|Y|Y|Y|Y|
|RedHat Enterprise Linux 8      |Y|Y| | | | | | |
|SUSE Linux Enterprise Server 11<sup>1</sup>|Y|Y|Y|Y|Y|Y|Y|Y|
|SUSE Linux Enterprise Server 12|Y|Y|Y|Y|Y|Y|Y|Y|
|SUSE Linux Enterprise Server 15|Y|Y|Y| | | | | |
|Ubuntu Linux 14.04             | |Y|Y|Y|Y|Y|Y|Y|
|Ubuntu Linux 16.04             |Y|Y|Y|Y|Y|Y|Y|Y|
|Ubuntu Linux 18.04             |Y|Y|Y|Y| | | | |
|Ubuntu Linux 19.10             |Y| | | | | | | |

<sup>1</sup> La versión 17 del controlador ODBC solo es compatible con SUSE Linux Enterprise Server 11 SP4

Los paquetes de instalación del [!INCLUDE[msCoName](../../../includes/msconame_md.md)] controlador ODBC 13, 13.1 y 17 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS resuelven las dependencias del controlador de forma automática cuando se instala con el sistema de administración de paquetes de la distribución, como se describe en [Instalación del controlador ODBC (Linux)](installing-the-microsoft-odbc-driver-for-sql-server.md) e [Instalación del controlador ODBC (macOS)](install-microsoft-odbc-driver-sql-server-macos.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Controlador ODBC 11 de Microsoft para SQL Server  
  
* Administrador de controladores unixODBC 2.3.0 de 64 bits creado para SQLLEN/SQLULEN de 64 bits. Las versiones posteriores del Administrador de controladores unixODBC de 64 bits no son compatibles con el controlador ODBC en Linux. Consulte [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) para obtener más información.  
  
* El controlador ODBC para **Red Hat Enterprise Linux 5 (64 bits)** requiere los siguientes paquetes y puede descargarse aquí: [Microsoft ODBC Driver 11 for SQL Server: Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321).  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `e2fsprogs-libs`  
  * `krb5-libs`  
  * `openssl`  
  
* El controlador ODBC para **Red Hat Enterprise Linux 6 (64 bits)** requiere los siguientes paquetes y puede descargarse aquí: [Microsoft ODBC Driver 11 for SQL Server: Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321).  
  * `glibc`  
  * `libgcc`  
  * `libstdc++`  
  * `libuuid`  
  * `krb5-libs`  
  * `openssl`  
  
* El controlador ODBC para **SUSE Linux Enterprise 11 Service Pack 2 (64 bits)** requiere los siguientes paquetes y puede descargarse aquí: [Microsoft ODBC Driver 11 Preview for SQL Server: SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
  * `glibc`  
  * `libstdc++46`  
  * `libgcc46`  
  * `libuuid1`  
  * `krb5`  
  * `libopenssl0_9_8`  
  
## <a name="see-also"></a>Consulte también

[Instalación del Administrador de controladores](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)  
[Problemas conocidos en esta versión del controlador](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  
[Notas de la versión](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
