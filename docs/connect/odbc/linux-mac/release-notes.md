---
title: 'Notas de la versión: Microsoft ODBC Driver for SQL Server en Linux y macOS | Microsoft Docs'
ms.custom: ''
ms.date: 06/29/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: 62270c3cce4b1a5f57874d6cd40c7c64ff409100
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600305"
---
# <a name="release-notes-for-the-microsoft-odbc-driver-for-sql-server-on-linux-and-macos"></a>Notas de la versión de Microsoft ODBC Driver for SQL Server en Linux y macOS
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS

**Nuevo distribuciones compatibles**: 18.04 Ubuntu

**Características agregadas**:

Clasificación de datos para Azure SQL Database y SQL Server, para obtener más información consulte [clasificación de datos](../data-classification.md)

Admite la codificación UTF-8 del servidor

SQLBrowseConnect

Dependencia dinámica de `libcurl`:
- A partir de esta versión, el `libcurl` paquete no es una dependencia explícita. El `libcurl` del paquete de OpenSSL o NSS es necesaria al usar la autenticación de Azure Key Vault o Azure Active Directory. Si se produce un error referente a `libcurl`, asegúrese de está instalado.

Idle Connection Resiliency con ConnectRetryCount y ConnectRetryInterval palabras clave de cadena de conexión (para obtener más información, consulte [resistencia de conexión en el controlador ODBC de Windows](../windows/connection-resiliency-in-the-windows-odbc-driver.md)):
- Use `SQL_COPT_SS_CONNECT_RETRY_COUNT`(solo lectura) para recuperar el número de reintentos de conexión.
- Use `SQL_COPT_SS_CONNECT_RETRY_INTERVAL`(solo lectura) para recuperar la longitud del intervalo de reintento de conexión.
- Una vez se volverá a conexión de forma predeterminada.


[Correcciones de errores](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS

**Características agregadas**:

Compatibilidad con `SQL_COPT_SS_CEKCACHETTL` y `SQL_COPT_SS_TRUSTEDCMKPATHS` los atributos de conexión (para obtener más información, consulte [uso de Always Encrypted con el controlador ODBC para SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Permite controlar el momento en que existe la memoria caché local de las claves de cifrado de columna, así como lo vaciado
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Permite que la aplicación restringir las operaciones de AE para que solo use la lista especificada de claves maestras de columna



Soporte técnico para cargar el `.rll` desde la ubicación predeterminada (para obtener más información, consulte [sección 'Cargar archivo de recursos' en el documento de instalación](installing-the-microsoft-odbc-driver-for-sql-server.md#resource-file-loading))

[Correcciones de errores](../bug-fixes.md)



## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS

**Nuevo distribuciones compatibles**: macOS High Sierra y con Ubuntu 17.10 

**Mejoras de rendimiento**: mayor que 10 veces la mejora del rendimiento cuando el controlador convierte hacia y desde UTF-8 o 16.

**Características agregadas**:

Compatibilidad con Always Encrypted para BCP API

Nuevo atributo de cadena de conexión UseFMTOnly hace el controlador utiliza los metadatos heredados en casos especiales que requieren las tablas temporales.

Compatibilidad con instancia administrada de SQL Azure (versión preliminar privada extendida). 
> [!NOTE]
> Hay varias diferencias cuando se usa la instancia administrada:
> -   No se admite FILESTREAM 
> -   Acceso de sistema de archivos local no admite, pero es necesario para cosas como tracefiles 
> -   Crear el UDT desde local no se admite la ruta de acceso 
> -   No se admite la autenticación integrada de Windows 
> -   DTC no se admite 
> -   cuenta 'sa' no está presente (cuenta predeterminada se denomina 'cloudSA')
> -   ERROR de token TDS (0xAA) devuelve el nombre de servidor incorrecto
> -   No se admiten caracteres especiales en el nombre de la base de datos 
> -   ALTER DATABASE [dbname1] MODIFY NAME = [dbname2] no es compatible
> -   Los mensajes de error siempre se muestran en inglés, independientemente del lenguaje de configuración (igual que Azure) 

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-linux-and-macos"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux y macOS  

ODBC Driver 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agrega compatibilidad con Always Encrypted y Azure Active Directory cuando se usa junto con Microsoft SQL Server 2016.

**Nuevo distribuciones compatibles**: OS X 10.11 y macOS 10.12 se admiten en la primera versión del controlador ODBC en macOS. Ubuntu 16.10 ahora también se admite, junto con Red Hat 6, 7 y SUSE 12. Cada plataforma tiene un paquete de plataforma correspondiente (RPM o DEB) para facilitar la instalación y configuración.  Consulte [instalar el controlador](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para obtener instrucciones de instalación.

**los cambios de compatibilidad 2.3.1 del Administrador de controladores unixODBC**: controlador ODBC ya no depende de empaquetado personalizada para el Administrador de controladores unixODBC (excepto en Red Hat 6) y en su lugar se basa en el Administrador de paquetes de distribución para resolver la dependencia de UnixODBC desde repositorios de la distribución.

**Compatibilidad con la API BCP**: controlador ODBC de Linux y macOS ahora admite el uso de la [funciones de la API de BCP (**bcp_init**, etcetera.)](../../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)

## <a name="whats-new-in-the-microsoft-odbc-driver-130-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>Novedades de Microsoft ODBC Driver 13.0 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux  
Con Microsoft ODBC Driver 13.0 para SQL Server, SQL Server 2014 y SQL Server 2016 ahora también se admiten.  

**Nuevo distribuciones compatibles**:

Junto con Red Hat y SUSE, ahora también se ofrece compatibilidad con Ubuntu. Cada plataforma tiene un paquete de plataforma correspondiente (RPM o DEB) para facilitar la instalación y configuración.  Consulte [instalar el controlador](../../../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md) para obtener instrucciones de instalación.

**compatibilidad con 2.3.1 del Administrador de controladores unixODBC**: además de un administrador de controladores más reciente, también hay un paquete para la instalación de esta dependencia que facilita la instalación y configuración.  

**Resolución de direcciones IP de red transparente**: resolución de direcciones IP de red transparente es una revisión de la característica de conmutación por error de múltiples subredes existente que afecta a la secuencia de conexión del controlador en el caso donde el primero resuelve IP del nombre de host no responder y hay varias direcciones IP asociada con el nombre de host.

**Soporte de TLS 1.2**: Microsoft ODBC Driver 13.0 for SQL Server en Linux admite ahora TLS 1.2, cuando se usan las comunicaciones seguras con SQL Server.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-linux"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Linux  
El controlador ODBC en SUSE Linux (Preview) es compatible con SUSE Linux Enterprise 11 Service Pack 2 de 64 bits. Para obtener más información, consulte [System Requirements](../../../connect/odbc/linux-mac/system-requirements.md).  

El controlador ODBC en Linux es compatible con [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]. Para obtener más información, vea [Compatibilidad del controlador ODBC con alta disponibilidad y recuperación ante desastres](../../../connect/odbc/linux-mac/odbc-driver-on-linux-support-for-high-availability-disaster-recovery.md).  

El controlador ODBC en Linux es compatible con conexiones a Base de datos SQL de Microsoft Azure. Para obtener más información, consulte [How to: Connect to Windows Azure SQL Database Using ODBC](https://msdn.microsoft.com/library/hh974312.aspx)(Cómo conectarse a Base de datos SQL de Windows Azure con ODBC).  

El `-l` ha agregado la opción (tiempo de espera de inicio de sesión) para `bcp`. Para obtener más información, vea [Conexión con **bcp**](../../../connect/odbc/linux-mac/connecting-with-bcp.md).
