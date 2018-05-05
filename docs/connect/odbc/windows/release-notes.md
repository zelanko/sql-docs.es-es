---
title: Notas (controlador ODBC para SQL Server) | Documentos de Microsoft
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b8459ed8-625e-4d8b-891c-e7e78c9977cc
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21380decd228d82695c4ca9972852585a4fc3dbc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="release-notes"></a>Notas de la versión
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

  Notas de la versión de Microsoft ODBC Driver for SQL Server en Windows.  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Novedades el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 17.1 el controlador ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows

**Características agregadas**:

Compatibilidad con `SQL_COPT_SS_CEKCACHETTL` y `SQL_COPT_SS_TRUSTEDCMKPATHS` atributos de conexión (para obtener más información, consulte [usar Always Encrypted con el controlador ODBC para SQL Server](../using-always-encrypted-with-the-odbc-driver.md))
- `SQL_COPT_SS_CEKCACHETTL` Permite controlar el momento en que existe la memoria caché local de las claves de cifrado de columna, así como el vaciado de él
- `SQL_COPT_SS_TRUSTEDCMKPATHS` Permite que la aplicación restringir las operaciones de AE para usar únicamente la lista especificada de claves maestras de columna


Compatibilidad con la autenticación interactiva de Azure Active Directory

[Correcciones de errores](../bug-fixes.md)


## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Novedades el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] 17 el controlador ODBC para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows

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
  

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-131-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Novedades el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13.1 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows  
 ODBC Driver 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] agrega compatibilidad para [Always Encrypted](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md) y [Azure Active Directory](../../../connect/odbc/using-azure-active-directory.md) cuando se utiliza junto con Microsoft SQL Server 2016.  Conexión correspondiente se describen los atributos y palabras clave de agrupación en [controlador compatible con agrupación de conexiones en el controlador ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md).

 ## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-13-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Novedades el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows  
 ODBC Driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] incluye la funcionalidad anterior de ODBC Driver 11 para SQL Server y agrega compatibilidad para Microsoft SQL Server 2016.

## <a name="whats-new-in-the-includemsconameincludesmsconamemdmd-odbc-driver-11-for-includessnoversionincludesssnoversionmdmd-on-windows"></a>Novedades el [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Windows  
 ODBC Driver 11 for SQL Server contiene nuevos [características](./features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md) , así como todas las características que se incluyen con ODBC en SQL Server 2012 Native Client.  
