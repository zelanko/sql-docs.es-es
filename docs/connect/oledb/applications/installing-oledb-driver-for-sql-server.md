---
title: Instalar el controlador OLE DB para SQL Server | Documentos de Microsoft
description: Instalar y desinstalar el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 0993eb185030e2573c3b2b25eddc9db055202596
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/03/2018
---
# <a name="installing-ole-db-driver-for-sql-server"></a>Instalar el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Para instalar al controlador OLE DB para SQL Server necesita a msoledbsql.msi instalador.
Ejecute el programa de instalación y realice las selecciones preferidas. El controlador OLE DB para SQL Server puede ser instalado en paralelo con versiones anteriores de los proveedores OLE DB de Microsoft.

Para descargar la versión más reciente del controlador OLE DB para SQL Server, vaya a [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=56730).

El controlador OLE DB para los archivos de SQL Server (msoledbsql.dll, msoledbsqlr.rll) se instalan en la siguiente ubicación:  

`%SYSTEMROOT%\system32\`  

> [!NOTE]  
> Toda la configuración del Registro adecuados para el controlador OLE DB para SQL Server se realiza como parte del proceso de instalación.  

El controlador OLE DB para SQL Server encabezado y biblioteca de archivos (msoledbsql.h y msoledbsql.lib) se instalan en la ubicación siguiente:  

`%PROGRAMFILES%\Microsoft SQL Server\Client SDK\OLEDB\180\SDK`  

Puede distribuir el controlador OLE DB para SQL Server a través de msoledbsql.msi. Es posible que deba instalar el controlador OLE DB para SQL Server al implementar una aplicación. Una manera de instalar varios paquetes en lo que al usuario le parece ser una instalación única es usar tecnología de encadenador y arranque. Para obtener más información, consulte [crear un paquete de arranque personalizado para Visual Studio 2005](http://go.microsoft.com/fwlink/?LinkId=115667) y [Agregar requisitos previos personalizados](http://go.microsoft.com/fwlink/?LinkId=115668).  
  
El x64 msoledbsql.msi también instala la versión de 32 bits del controlador de OLE DB para SQL Server. Si la aplicación tiene como destino una plataforma distinta a la que se desarrolló, puede descargar versiones de msoledbsql.msi para x64 y x86.

Cuando se invoca msoledbsql.msi, sólo los componentes de cliente se instalan de forma predeterminada. El cliente son componentes son archivos que permiten ejecutar aplicaciones desarrolladas mediante el controlador OLE DB para SQL Server. Para instalar también los componentes SDK, especifique `ADDLOCAL=All` en la línea de comandos. Por ejemplo:  

`msiexec /i msoledbsql.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

## <a name="silent-install"></a>Instalación silenciosa  
 Si usas el/passive/qn, /qb o/QR opción con msiexec, también debe especificar IACCEPTMSOLEDBSQLLICENSETERMS = Sí, para indicar explícitamente que acepta los términos de la licencia de usuario final. Esta opción se debe especificar con todas las letras mayúsculas.  

## <a name="uninstalling-ole-db-driver-for-sql-server"></a>Desinstalar el controlador OLE DB para SQL Server  
Dado que aplicaciones como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servidor y el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herramientas dependen de controlador de OLE DB para SQL Server, es importante no desinstalar el controlador OLE DB para SQL Server hasta que se desinstalen todas las aplicaciones dependientes. Para proporcionar a los usuarios con una advertencia de que la aplicación depende de controlador de OLE DB para SQL Server, use la opción de instalación APPGUID en su MSI, como se indica a continuación:  

 `msiexec /i msoledbsql.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  

El valor pasado a APPGUID es su código de producto específico. Se debe crear un código de producto al usar Microsoft Installer para empaquetar su programa de instalación de la aplicación.  

## <a name="see-also"></a>Vea también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
