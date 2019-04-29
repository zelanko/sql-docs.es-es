---
title: Instalar SQL Server Native Client | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, uninstalling
- SQLNCLI, installing
- SQLNCLI, uninstalling
- Setup [SQL Server Native Client]
- uninstalling SQL Server Native Client
- data access [SQL Server Native Client], uninstalling SQL Server Native Client
- installing SQL Server Native Client
- SQL Server Native Client, installing
- data access [SQL Server Native Client], installing SQL Server Native Client
- removing SQL Server Native Client
ms.assetid: c6abeab2-0052-49c9-be79-cfbc50bff5c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71438a61dcaec201d0b3ae21eb7e27d979029204
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046360"
---
# <a name="installing-sql-server-native-client"></a>Instalar SQL Server Native Client
  Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 se instala a la vez que [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]. No hay ningún [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] Native Client. Para obtener más información, consulte [What ' s New in SQL Server Native Client](../sql-server-native-client.md). También puede obtener sqlncli.msi de la página web de SQL Server 2012 Feature Pack. Para descargar la versión más reciente de SQL Server Native Client, vaya a [Microsoft?? ¿SQL Server? 2012 SP2 Feature Pack de](https://www.microsoft.com/en-us/download/details.aspx?id=43339). Si también está instalada una versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client anterior a SQL Server 2012 en el equipo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 11.0 se instalará en paralelo con la versión anterior.  
  
 Los archivos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli11.dll, sqlnclir11.rll y s11ch_sqlncli.chm) se instalan en la siguiente ubicación:  
  
 `%SYSTEMROOT%\system32\`  
  
> [!NOTE]  
>  Todos los valores del Registro adecuados para el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se crean como parte del proceso de instalación.  
  
 Los archivos de encabezado y biblioteca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h y sqlncli11.lib) se instalan en la siguiente ubicación:  
  
 `%PROGRAMFILES%\Microsoft SQL Server\110\SDK`  
  
 Además de instalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como parte de la instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], hay también un programa de instalación redistribuible denominado sqlncli.msi, que se puede encontrar en el disco de instalación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la ubicación siguiente: `%CD%\Setup\`.  
  
 Puede distribuir [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a través de sqlncli.msi. Es posible que tenga que instalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client al implementar una aplicación. Una manera de instalar varios paquetes en lo que al usuario le parece ser una instalación única es usar tecnología de encadenador y arranque. Para obtener más información, vea [Authoring a Custom Bootstrapper Package for Visual Studio 2005](https://go.microsoft.com/fwlink/?LinkId=115667) (Crear un paquete de arranque personalizado para Visual Studio 2005) y [Adding Custom Prerequisites](https://go.microsoft.com/fwlink/?LinkId=115668) (Agregar requisitos previos personalizados).  
  
 Las versiones x64 e Itanium de sqlncli.msi también instalan las versiones de 32 bits de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Si su aplicación está diseñada para una plataforma distinta de aquella en la que se desarrolló, puede descargar versiones de sqlncli.msi para x64, Itanium y x86 en el Centro de descarga de Microsoft.  
  
 Cuando se llama a sqlncli.msi, solo se instalan los componentes de cliente de forma predeterminada. Los componentes de cliente son archivos que admiten la ejecución de una aplicación que se desarrolló con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Para instalar también los componentes SDK, especifique `ADDLOCAL=All` en la línea de comandos. Por ejemplo:  
  
 `msiexec /i sqlncli.msi ADDLOCAL=ALL APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
## <a name="silent-install"></a>Instalación silenciosa  
 Si usa la opción /passive, /qn, /qb o /qr con msiexec, también debe especificar IACCEPTSQLNCLILICENSETERMS=YES, para indicar explícitamente que acepta los términos de la licencia de usuario final. Esta opción se debe especificar con todas las letras mayúsculas.  
  
## <a name="uninstalling-sql-server-native-client"></a>Desinstalar SQL Server Native Client  
 Dado que aplicaciones como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] server y el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dependen de las herramientas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, es importante no desinstalar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client hasta que se desinstalen todas las aplicaciones dependientes. Para usuarios con una advertencia de que la aplicación depende del proveedor [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, utilice la opción de instalación APPGUID en su MSI, como se indica a continuación:  
  
 `msiexec /i sqlncli.msi APPGUID={0CC618CE-F36A-415E-84B4-FB1BFF6967E1}`  
  
 El valor pasado a APPGUID es su código de producto específico. Se debe crear un código de producto al usar Microsoft Installer para empaquetar su programa de instalación de la aplicación.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con SQL Server Native Client](installing-sql-server-native-client.md)   
 [Temas de procedimientos de instalación](../../../sql-server/install/installation-how-to-topics.md)  
  
  
