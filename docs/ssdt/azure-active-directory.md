---
title: Compatibilidad de Azure Active Directory con SQL Server Data Tools (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 04/09/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: ssdt
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 906bd42a1a4143217a974dd114adf82fa41e7270
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2018
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>Compatibilidad de Azure Active Directory con SQL Server Data Tools (SSDT)

[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md.md](../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

SQL Server Data Tools (SSDT) proporciona varios métodos de autenticación de [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis).

![Cuadro de diálogo de conexión de SSDT](media/azure-active-directory/interactive.png)

## <a name="active-directory-password-authentication"></a>Autenticación de contraseña de Active Directory

Autenticación de contraseña de Active Directory es un mecanismo que permite conectarse con Azure SQL Database mediante identidades de Azure Active Directory (Azure AD).  Use este método para conectarse si ha iniciado sesión en Windows con credenciales de un dominio no federado con Azure o si usa la autenticación de Azure AD con Azure AD basado en el dominio inicial o de cliente. Para más información, consulte [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).  

## <a name="active-directory-integrated-authentication"></a>Autenticación integrada de Active Directory

Autenticación integrada de Active Directory es un mecanismo que permite conectarse con Azure SQL Database mediante identidades de Azure Active Directory (Azure AD). Use este método para conectarse si ha iniciado sesión en Windows con credenciales de Azure Active Directory de un dominio federado. Para más información, consulte [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="active-directory-interactive-authentication"></a>Autenticación interactiva de Active Directory

SSDT proporciona un método de autenticación nuevo para conectarse a una instancia de Azure SQL Database, **Autenticación interactiva de Active Directory**.


> [!NOTE]
> Autenticación interactiva de Active Directory está disponible al conectarse con SSDT en [Visual Studio 2017, versión 15.6](https://docs.microsoft.com/visualstudio/releasenotes/vs2017-relnotes) y requiere [descargar e instalar .NET Framework 4.7.2](https://www.microsoft.com/net/download/all) en el equipo que ejecuta SSDT. Si no está instalada la versión preliminar de [.NET Framework 4.7.2](https://docs.microsoft.com/dotnet/api/?view=netframework-4.7.2), la opción Autenticación interactiva de Active Directory no estará disponible.


Autenticación interactiva de Active Directory admite una autenticación interactiva que permite usar Multi-Factor Authentication (MFA) de Azure Active Directory (AD) para autenticarse con Azure SQL Database. Este método admite a los usuarios de Azure AD nativos y federados y usuarios invitados de otras cuentas (incluidos usuarios B2B, cuentas Microsoft y cuentas que no son de Microsoft, como @outlook.com, @hotmail.com, @live.com, así como también @gmail.com). Si se especifica este método, se debe especificar el **nombre de usuario** y se deshabilitará el campo Contraseña. 

Al autenticarse con *Autenticación interactiva de Active Directory*, se abre una ventana de autenticación en la que los usuarios deben escribir manualmente una contraseña.

![Cuadro de diálogo de inicio de sesión](media/azure-active-directory/sign-in.png)

Azure AD proporciona la aplicación de MFA a través de esta ventana emergente de MFA adicional durante el proceso de autenticación.

> [!NOTE]
> Como *Autenticación interactiva de Active Directory* requiere que los usuarios escriban de manera manual (interactivamente) la contraseña, no se recomienda para los flujos de trabajo automatizados.


## <a name="known-issues-and-limitations"></a>Limitaciones y problemas conocidos

- *Autenticación interactiva de Active Directory* solo se admite al conectarse a una instancia de Azure SQL Database. No es compatible con SQL Server (ni local ni en una máquina virtual) ni con Azure SQL Data Warehouse.
- *Autenticación interactiva de Active Directory* no se admite en el cuadro de diálogo de conexión en el *Explorador de servidores*, debe conectarse mediante SSDT con el *Explorador de objetos de SQL Server*.
- La integración del inicio de sesión único con la cuenta de Visual Studio que inició la sesión no es compatible con SSDT.
- El archivo SQLPackage.exe que se instaló en el directorio de extensiones durante la instalación de Visual Studio no está pensado para usarlo desde esa ubicación. Para usar SQLpackage.exe con AAD, vaya a https://www.microsoft.com/en-us/download/details.aspx?id=55088 
- La comparación de datos de SSDT no es compatible con la autenticación de AAD, incluido el método de autenticación nuevo.  





## <a name="see-also"></a>Ver también  
[Autenticación multifactor](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)  
[Autenticación de Azure Active Directory con SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)  
[Herramientas de datos de SQL Server](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)  
[Foro MSDN de SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog del equipo de SSDT](http://blogs.msdn.com/b/ssdt/)  
[Referencia de la API de DACFx](https://msdn.microsoft.com/library/dn645454.aspx)  
[Descarga de SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
