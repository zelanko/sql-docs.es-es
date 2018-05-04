---
title: Notas - Microsoft ODBC Driver for SQL Server en Linux y macOS | Documentos de Microsoft
ms.custom: ''
ms.date: 04/04/2018
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65dca8aaaf21233419b07d055ed6bf68afa5dfef
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Notas de la versión para Microsoft ODBC Driver for SQL Server en Linux y Mac OS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Novedades el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 17.1 el controlador ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows

**Características agregadas**:

Compatibilidad con `SQL_COPT_SS_CEKCACHETTL` y `SQL_COPT_SS_TRUSTEDCMKPATHS` atributos de conexión (para obtener más información, consulte [usar Always Encrypted con el controlador ODBC para SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Permite controlar el momento en que existe la memoria caché local de las claves de cifrado de columna, así como el vaciado de él
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Permite que la aplicación restringir las operaciones de AE para usar únicamente la lista especificada de claves maestras de columna



Soporte para cargar la `.rll` desde la ubicación predeterminada (para obtener más información, consulte [sección 'Cargar archivo de recursos' en el documento de instalación](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading))

[Correcciones de errores](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-linux-and-macos"></a>Novedades el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 17 del controlador de ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Linux y Mac OS

**Nuevo distribuciones admitidas**: macOS Sierra alta y Ubuntu 17.10 

**Mejoras de rendimiento**: mayor que 10 x mejora del rendimiento al controlador convierte de UTF-8 o 16.

**Características agregadas**:

Always Encrypted compatibilidad con API de BCP

Nuevo atributo de cadena de conexión UseFMTOnly hace controlador utilizar los metadatos heredados en casos especiales que requieren tablas temporales.

Compatibilidad con la instancia administrada de SQL Azure (vista previa privada extendida). 
> [!NOTE]
> Hay varias diferencias cuando se usa la instancia administrada:
> -   No se admite FILESTREAM 
> -   Acceso de sistema de archivos local no se admiten, pero se necesitan para cosas como tracefiles 
> -   Crear el UDT local no se admite la ruta de acceso 
> -   No se admite la autenticación integrada de Windows 
> -   No se admite el DTC 
> -   cuenta 'sa' no está presente (cuenta predeterminada se denomina 'cloudSA')
> -   ERROR de símbolo (token) de TDS (0xAA) devuelve el nombre de servidor incorrecto
> -   No se admiten caracteres especiales en el nombre de la base de datos 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] no es compatible
> -   Los mensajes de error siempre se muestran en inglés, independientemente del lenguaje configuración (igual que Azure) 

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
