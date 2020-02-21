---
title: Instalación del controlador OLE DB para SQL Server | Microsoft Docs
description: Instalación y desinstalación de OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, uninstalling
- MSOLEDBSQL, installing
- MSOLEDBSQL, uninstalling
- Setup [OLE DB Driver for SQL Server]
- uninstalling OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], uninstalling OLE DB Driver for SQL Server
- installing OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, installing
- data access [OLE DB Driver for SQL Server], installing OLE DB Driver for SQL Server
- removing OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 08f33d84ee8c035e1e1d3818e2a036f96af2a280
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67989309"
---
# <a name="installing-ole-db-driver-for-sql-server"></a>Instalación del controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Para instalar OLE DB Driver for SQL Server necesita el instalador de msoledbsql.msi.
Ejecute el instalador y realice las selecciones preferidas. OLE DB Driver for SQL Server se puede instalar en paralelo con versiones anteriores de los proveedores de Microsoft OLE DB.

Los archivos de OLE DB Driver for SQL Server (msoledbsql.dll, msoledbsqlr.rll) se instalan en `%SYSTEMROOT%\system32\`. Además, msoledbsql.msi de x64 instala los archivos binarios de 32 bits en `%SYSTEMROOT%\SysWOW64\`.

> [!NOTE]  
> Como parte del proceso de instalación, se realiza la configuración adecuada del Registro para OLE DB Driver for SQL Server.  

Los archivos de encabezado y los de biblioteca de OLE DB Driver for SQL Server (msoledbsql.h y msoledbsql.lib) se instalan en `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`. Además, el archivo msoledbsql.msi de x64 instala los mismos archivos en `%PROGRAMFILES(x86)%\Microsoft SQL Server\Client SDK\OLEDB\182\SDK`.  

Puede distribuir OLE DB Driver for SQL Server a través de msoledbsql.msi. Es posible que tenga que instalar OLE DB Driver for SQL Server al implementar una aplicación. Una manera de instalar varios paquetes en lo que al usuario le parece ser una instalación única es usar tecnología de encadenador y arranque. Para obtener más información, vea [Authoring a Custom Bootstrapper Package for Visual Studio 2005](https://go.microsoft.com/fwlink/?LinkId=115667) (Crear un paquete de arranque personalizado para Visual Studio 2005) y [Adding Custom Prerequisites](https://go.microsoft.com/fwlink/?LinkId=115668) (Agregar requisitos previos personalizados).  
  
El archivo msoledbsql.msi de x64 también instala la versión de 32 bits de OLE DB Driver for SQL Server. Si la aplicación está diseñada para una plataforma distinta de aquella en la que se desarrolló, puede descargar versiones de msoledbsql.msi para x64 y x86.

Cuando se invoca a msoledbsql.msi, solo los componentes cliente se instalan de forma predeterminada. Los componentes cliente son archivos que permiten la ejecución de una aplicación que se ha desarrollado mediante el controlador OLE DB para SQL Server. Para instalar también los componentes SDK, especifique `ADDLOCAL=All` en la línea de comandos. Por ejemplo:  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL`  

## <a name="silent-install"></a>Instalación silenciosa  
 Si usa las opciones /passive, /qn, /qb o /qr con msiexec, también debe especificar IACCEPTMSOLEDBSQLLICENSETERMS=YES para indicar explícitamente que acepta los términos de la licencia de usuario final. Esta opción se debe especificar con todas las letras mayúsculas.  

## <a name="installing-ole-db-driver-for-sql-server-as-a-dependency"></a>Instalación de OLE DB Driver for SQL Server como una dependencia  
Es importante no desinstalar OLE DB Driver for SQL Server hasta que se desinstalen todas las aplicaciones dependientes. Para proporcionar a los usuarios una advertencia de que la aplicación depende de OLE DB Driver for SQL Server, use la opción de instalación APPGUID en su MSI, de la siguiente manera:  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

El valor pasado a APPGUID es su código de producto específico. Se debe crear un código de producto al usar Microsoft Installer para empaquetar su programa de instalación de la aplicación.
La opción APPGUID requiere ejecutar el instalador desde un símbolo del sistema con privilegios elevados.

## <a name="see-also"></a>Consulte también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
