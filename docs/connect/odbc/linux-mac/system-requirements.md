---
title: Requisitos del sistema (controlador ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/15/2018
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b7e2dde267cf2c5f12140d883114565390d2e5d6
ms.sourcegitcommit: e821cd8e5daf95721caa1e64c2815a4523227aa4
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68702711"
---
# <a name="system-requirements"></a>Requisitos del sistema
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

En este tema se muestran los requisitos para utilizar [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y MacOS.


## <a name="microsoft-odbc-driver-13-131-and-17-for-sql-server"></a>Microsoft ODBC Driver 13, 13.1 y 17 for SQL Server

Los controladores de Linux y macOS están disponibles solamente para las versiones de 64 bits de los siguientes sistemas operativos:

|Sistema operativo|Versión del controlador compatible|
|------------------------------------|--------------------------------|
|Apple OS X 10.11 (El Capitan)|13, 13.1, 17|
|Apple macOS 10.12 (Sierra)|13, 13.1, 17|
|Apple macOS 10.13 (High Sierra)|17| 
|Apple macOS 10.14 (Mojave)|17| 
|Debian Linux 8|13, 13.1, 17|
|Debian Linux 9|17|
|Debian Linux 10|17.4|
|RedHat Enterprise Linux 6|13, 13.1, 17|
|RedHat Enterprise Linux 7|13, 13.1, 17|
|RedHat Enterprise Linux 8|17.4|
|SuSE Linux Enterprise Server 11|13, 13.1, 17 <br /><br /> **Nota:** La versión 17 del controlador ODBC solo es compatible con SuSE Linux Enterprise Server 11 SP4|
|SuSE Linux Enterprise Server 12|13, 13.1, 17|
|SuSE Linux Enterprise Server 15|17|
|Ubuntu Linux 14.04|13, 13.1, 17|
|Ubuntu Linux 15.10|13, 13.1|
|Ubuntu Linux 16.04|13, 13.1, 17|
|Ubuntu Linux 16.10|13, 13.1|
|Ubuntu Linux 17.04|17| 
|Ubuntu Linux 17.10|17|
|Ubuntu Linux 18.04|17| 
|Ubuntu Linux 18.10|17| 
|Ubuntu Linux 19.04|17.3| 

La instalación de paquetes del controlador ODBC de [!INCLUDE[msCoName](../../../includes/msconame_md.md)], versiones 13, 13.1 y 17 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS, resuelve las dependencias del controlador automáticamente cuando se instala con el sistema de administración de paquetes de la distribución, tal como se describe en [Instalación del controlador](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Controlador ODBC 11 de Microsoft para SQL Server  
  
-   Administrador de controladores unixODBC 2.3.0 de 64 bits creado para SQLLEN/SQLULEN de 64 bits. Las versiones posteriores del Administrador de controladores unixODBC de 64 bits no son compatibles con el controlador ODBC en Linux. Consulte [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) para obtener más información.  
  
-   El controlador ODBC para **Red Hat Enterprise Linux 5 (64 bits)** requiere los siguientes paquetes y puede descargarse aquí: [Microsoft ODBC Driver 11 for SQL Server: Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321).  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `e2fsprogs-libs`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   El controlador ODBC para **Red Hat Enterprise Linux 6 (64 bits)** requiere los siguientes paquetes y puede descargarse aquí: [Microsoft ODBC Driver 11 for SQL Server: Red Hat Linux](https://go.microsoft.com/fwlink/?LinkId=267321).  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `libuuid`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   El controlador ODBC para **SUSE Linux Enterprise 11 Service Pack 2 (64 bits)** requiere los siguientes paquetes y puede descargarse aquí: [Microsoft ODBC Driver 11 Preview for SQL Server: SUSE Linux](https://go.microsoft.com/fwlink/?LinkId=264916)  
    -   `glibc`  
    -   `libstdc++46`  
    -   `libgcc46`  
    -   `libuuid1`  
    -   `krb5`  
    -   `libopenssl0_9_8`  
  
## <a name="see-also"></a>Consulte también
[Instalación del Administrador de controladores](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Problemas conocidos en esta versión del controlador](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
