---
title: Notas - Microsoft ODBC Driver for SQL Server en Linux y macOS | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: bc1321dd91a0fcb7ab76b207301c6302bb3a5e64
ms.openlocfilehash: 84bb78e184f1bca9e683aeebf46b178e3a7dd61f
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Notas de la versión para Microsoft ODBC Driver for SQL Server en Linux y Mac OS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-linux-and-macos"></a>Novedades el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux y Mac OS  

ODBC Driver 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] agrega compatibilidad con Always Encrypted y Azure Active Directory cuando se utiliza junto con Microsoft SQL Server 2016.

**Nuevo distribuciones admitidas**: OS X 10.11 y macOS 10.12 se admiten en la primera versión del controlador ODBC en macOS. Ubuntu 16,10 ahora también se admite, junto con Red Hat 6, 7 y 12 SUSE. Cada plataforma tiene un paquete relativas a la plataforma (RPM o DEB) para facilitar la instalación y configuración.  Vea [instalar el controlador](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para obtener instrucciones de instalación.

**Cambios de soporte técnico de 2.3.1 del Administrador de controladores unixODBC**: el controlador ODBC el ya no depende de empaquetado personalizada para el Administrador de controladores unixODBC (excepto en RedHat 6) y en su lugar se basa en el Administrador de paquetes de distribución para resolver la dependencia de UnixODBC desde repositorios de la distribución.

**Compatibilidad con la API de BCP**: controlador ODBC de Linux y macOS ahora admite el uso de la [funciones de la API de BCP (**bcp_init**, etcetera.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>Novedades de Microsoft ODBC Driver 13.0 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux  
Con Microsoft ODBC Driver 13.0 para SQL Server, SQL Server 2014 y SQL Server 2016 ahora también se admiten.  

**Nuevo distribuciones compatibles**:

Junto con Red Hat y SUSE, ahora también se ofrece compatibilidad con Ubuntu. Cada plataforma tiene un paquete relativas a la plataforma (RPM o DEB) para facilitar la instalación y configuración.  Vea [instalar el controlador](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para obtener instrucciones de instalación.

**compatibilidad con el Administrador de controladores 2.3.1 unixODBC**: además de un administrador de controladores más recientes, también hay un paquete para la instalación de esta dependencia que facilita la instalación y configuración.  

**Resolución de IP de red transparente**: resolución de IP de red transparente es una revisión de la característica de conmutación por error de múltiples subredes existente que afecta a la secuencia de conexión del controlador en el caso donde la primera resuelve la dirección IP del nombre de host no responder y hay varias direcciones IP asociadas con el nombre de host.

**Soporte de TLS 1.2**: The 13.0 de controlador ODBC de Microsoft para SQL Server en Linux admite ahora TLS 1.2, cuando se utilizan las comunicaciones seguras con SQL Server.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-linux"></a>Novedades el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux  
El controlador ODBC en SUSE Linux (Preview) es compatible con SUSE Linux Enterprise 11 Service Pack 2 de 64 bits. Para obtener más información, consulte [requisitos del sistema](../../../connect/odbc/linux-mac/system-requirements.md).  

El controlador ODBC en Linux es compatible con [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obtener más información, consulte [controlador ODBC en compatibilidad con Linux en High Availability, Disaster Recovery](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  

El controlador ODBC en Linux es compatible con conexiones a Base de datos SQL de Microsoft Azure. Para obtener más información, consulte [How to: Connect to Windows Azure SQL Database Using ODBC](http://msdn.microsoft.com/library/hh974312.aspx)(Cómo conectarse a Base de datos SQL de Windows Azure con ODBC).  

El `-l` opción (tiempo de espera de inicio de sesión) se ha agregado a `bcp`. Para obtener más información, consulte [conectar con **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md).

