---
title: Requisitos del sistema (controlador ODBC para SQL Server) | Documentos de Microsoft
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- prerequisites
- system requirements
- requirements
ms.assetid: f03b7fdd-0e9d-4e74-958d-e8c87e027348
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb3ccdb0348cc05146bdadbccb8ce26d733cea79
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="system-requirements"></a>Requisitos del sistema
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Este tema enumeran los requisitos para utilizar el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux y macOS.


## <a name="microsoft-odbc-driver-13-131-and-17-for-sql-server"></a>Microsoft ODBC Driver 13, 13.1 y 17 para SQL Server

Los controladores de Linux y macOS solo están disponibles para las versiones de 64 bits de los sistemas operativos siguientes:

|Sistema operativo|Versión de controlador compatible|
|------------------------------------|--------------------------------|
|Apple OS X 10.11 (El capitán)|13, 13.1, 17|
|Apple macOS 10.12 (Sierra)|13, 13.1, 17|
|Apple macOS 10.13 (Sierra alta)|17| 
|Debian Linux 8|13, 13.1, 17|
|Debian Linux 9|17|
|RedHat Enterprise Linux 6|13, 13.1, 17|
|RedHat Enterprise Linux 7|13, 13.1, 17|
|SuSE Linux Enterprise Server 11|13, 13.1, 17 <br /><br /> **Nota:** 17 del controlador ODBC solo admite SuSE Linux Enterprise Server 11 SP4|
|SuSE Linux Enterprise Server 12|13, 13.1, 17|
|Ubuntu Linux 14.04|13, 13.1, 17|
|Ubuntu Linux 15.10|13, 13.1|
|Ubuntu Linux 16.04|13, 13.1, 17|
|Ubuntu Linux 16,10|13, 13.1|
|Ubuntu Linux 17.10|17|

La instalación de paquetes para la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13, 13.1 y 17 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux y macOS resolver las dependencias del controlador automáticamente cuando se instalen con el sistema de administración del paquete de la distribución, como se describe en [ Instalar el controlador](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

## <a name="microsoft-odbc-driver-11-for-sql-server"></a>Controlador ODBC 11 de Microsoft para SQL Server  
  
-   Administrador de controladores unixODBC 2.3.0 de 64 bits creado para SQLLEN/SQLULEN de 64 bits. Las versiones posteriores del Administrador de controladores unixODBC de 64 bits no son compatibles con el controlador ODBC en Linux. Consulte [Installing the Driver Manager](../../../connect/odbc/linux-mac/installing-the-driver-manager.md) para obtener más información.  
  
-   El controlador ODBC para **Red Hat Enterprise Linux 5 (64 bits)** requiere los siguientes paquetes y puede descargarse aquí: [Microsoft ODBC Driver 11 for SQL Server: Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `e2fsprogs-libs`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   El controlador ODBC para **Red Hat Enterprise Linux 6 (64 bits)** requiere los siguientes paquetes y puede descargarse aquí: [Microsoft ODBC Driver 11 for SQL Server: Red Hat Linux](http://go.microsoft.com/fwlink/?LinkId=267321)  
    -   `glibc`  
    -   `libgcc`  
    -   `libstdc++`  
    -   `libuuid`  
    -   `krb5-libs`  
    -   `openssl`  
  
-   El controlador ODBC para **SUSE Linux Enterprise 11 Service Pack 2 (64 bits)** requiere los siguientes paquetes y puede descargarse aquí: [Preview de Microsoft ODBC Driver 11 for SQL Server: SUSE Linux](http://go.microsoft.com/fwlink/?LinkId=264916)  
    -   `glibc`  
    -   `libstdc++46`  
    -   `libgcc46`  
    -   `libuuid1`  
    -   `krb5`  
    -   `libopenssl0_9_8`  
  
## <a name="see-also"></a>Vea también
[Instalación del Administrador de controladores](../../../connect/odbc/linux-mac/installing-the-driver-manager.md)

[Problemas conocidos en esta versión del controlador](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)  

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)  
