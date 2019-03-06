---
title: Notas de la versión (Controlador ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/03/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
author: MightyPen
ms.author: v-jizho2
manager: kenvh
ms.openlocfilehash: cc1321ac161923499d57ab69374b8ed603d272e0
ms.sourcegitcommit: 2ab79765e51913f1df6410f0cd56bf2a13221f37
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/27/2019
ms.locfileid: "56955776"
---
# <a name="release-notes"></a>Notas de la versión
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Notas de la versión de Microsoft ODBC Driver for SQL Server en Windows.  


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-173-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novedades del [!INCLUDE[msCoName](../../../includes/msconame_md.md)] controlador ODBC 17.3 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows

**Características agregadas**:

- Azure Active Directory Managed Service Identity (sistema y usuario asignado) el modo de autenticación, para obtener más información, vea [mediante Azure Active Directory con el controlador ODBC](../using-azure-active-directory.md)
- Capacidad de transmitir los parámetros de entrada con columnas de Always Encrypted, para obtener más información, vea [limitaciones del controlador ODBC cuando se usa Always Encrypted](../using-always-encrypted-with-the-odbc-driver.md#limitations-of-the-odbc-driver-when-using-always-encrypted)
- XA transacciones distribuidas, para obtener más información, vea [uso de transacciones XA](../use-xa-with-dtc.md)

[Correcciones de errores](../bug-fixes.md)

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-172-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.2 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows

**Características agregadas**:

Clasificación de datos para Azure SQL Database y SQL Server, para obtener más información consulte [clasificación de datos](../data-classification.md)

Compatibilidad con codificación UTF-8 del servidor

[Correcciones de errores](../bug-fixes.md)

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows

**Características agregadas**:

Compatibilidad con `SQL_COPT_SS_CEKCACHETTL` y `SQL_COPT_SS_TRUSTEDCMKPATHS` los atributos de conexión (para obtener más información, consulte [uso de Always Encrypted con el controlador ODBC para SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Permite controlar el momento en que existe la memoria caché local de las claves de cifrado de columna, así como lo vaciado
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Permite que la aplicación restringir las operaciones de AE para que solo use la lista especificada de claves maestras de columna


Compatibilidad con la autenticación interactiva de Azure Active Directory

[Correcciones de errores](../bug-fixes.md)


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows

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
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows  
 ODBC Driver 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agrega compatibilidad para [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) y [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) cuando se usa junto con Microsoft SQL Server 2016.  Conexión correspondiente se describen los atributos o palabras clave de agrupación en [Aware Connection Pooling de controlador en el controlador ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows  
 ODBC Driver 13 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluye la funcionalidad anterior de ODBC Driver 11 para SQL Server y agrega compatibilidad para Microsoft SQL Server 2016.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Novedades de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en Windows  
 ODBC Driver 11 for SQL Server contiene [características](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md) nuevas y todas las que se incluyen con ODBC en SQL Server 2012 Native Client.  
