---
title: Azure Active Directory en SSDT
ms.prod: sql
ms.technology: ssdt
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: jroth
reviewer: ''
ms.custom: seo-lt-2019
ms.date: 10/28/2019
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: ed7bc77b48881351a144ed5d217454518abafcc2
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/13/2020
ms.locfileid: "79286209"
---
# <a name="azure-active-directory-support-in-sql-server-data-tools-ssdt"></a>Compatibilidad de Azure Active Directory con SQL Server Data Tools (SSDT)

[!INCLUDE[appliesto-xx-asdb-asdb-xxx-md.md](../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

SQL Server Data Tools (SSDT) proporciona varios métodos de autenticación de [Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/active-directory-whatis).

En Visual Studio, abra el **Explorador de objetos de SQL Server** (en el menú **Vista**) y seleccione **Agregar SQL Server**:

![Cuadro de diálogo de conexión de SSDT](media/azure-active-directory/interactive.png)

#### <a name="which-azure-sql-products"></a>¿Qué productos de Azure SQL?

En este artículo se describe Azure AD para la lista siguiente de *productos de Azure SQL* en [Azure Cloud](https://azure.microsoft.com/):

- Azure SQL Database
- Azure SQL Data Warehouse

## <a name="active-directory-password-authentication"></a>Autenticación de contraseña de Active Directory

*Autenticación de contraseña de Active Directory* es un mecanismo de conexión a los productos de Azure SQL mencionados anteriormente. El mecanismo usa identidades en Azure Active Directory (Azure AD). Use este método para la conexión cuando:

- Haya iniciado sesión en Windows con las credenciales de un dominio que no está federado con Azure, o bien
- Use la autenticación de Azure AD con Azure AD y se base en el dominio cliente o inicial.

Para más información, consulte [Usar la autenticación de Azure Active Directory para autenticación con SQL](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).  

## <a name="active-directory-integrated-authentication"></a>Autenticación integrada de Active Directory

*Autenticación integrada de Active Directory* es un mecanismo que permite conectarse a los productos de Azure SQL indicados mediante identidades de Azure Active Directory (Azure AD). Use este método para conectarse si ha iniciado sesión en Windows con credenciales de Azure Active Directory de un dominio federado. Para más información, consulte [Usar la autenticación de Azure Active Directory para autenticación con SQL](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

## <a name="active-directory-interactive-authentication"></a>Autenticación interactiva de Active Directory

*Autenticación interactiva de Active Directory* está disponible cuando se conecta a los productos de Azure SQL enumerados con SSDT, pero solo con [.NET Framework 4.7.2](https://docs.microsoft.com/dotnet/api/?view=netframework-4.7.2) o una versión posterior.

- [Descargar e instalar para cualquier versión de .NET Framework](https://www.microsoft.com/net/download/all).
- [Visual Studio 2017, versión 15.6](https://docs.microsoft.com/visualstudio/releasenotes/vs2017-relnotes) o una versión posterior.

#### <a name="multi-factor-authentication-mfa"></a>Multi-Factor Authentication (MFA)

Autenticación interactiva de Active Directory admite una autenticación interactiva que permite usar Multi-Factor Authentication (MFA) de Azure Active Directory (AD) para autenticarse con los productos enumerados de Azure SQL. Este método admite usuarios de Azure AD nativos y federados, y usuarios invitados de otras cuentas. Los otros tipos de cuenta incluyen:

- Usuarios de negocio a negocio (Azure AD B2B).
- Cuentas de Microsoft, como @outlook.com, @hotmail.com, @live.com.
- Cuenta que no sean de Microsoft, como @gmail.com.

Si se especifica el método MFA, se debe especificar el **nombre de usuario** y se deshabilitará el campo **Contraseña**. 

#### <a name="password-entry"></a>Entrada de contraseña

Al autenticarse con *Autenticación interactiva de Active Directory*, se abre una ventana de autenticación en la que los usuarios deben escribir manualmente una contraseña.

![Cuadro de diálogo de inicio de sesión](media/azure-active-directory/sign-in.png)

Azure AD proporciona la aplicación de MFA a través de esta ventana emergente de MFA adicional.

> [!NOTE]
> Los flujos de trabajo automatizados se bloquearían mediante el uso de *Autenticación interactiva de Active Directory*. Debe haber una persona disponible para interactuar con el proceso de autenticación, para que escriba una contraseña de forma manual.

## <a name="known-issues-and-limitations"></a>Limitaciones y problemas conocidos

- *Autenticación interactiva de Active Directory* solo se admite al conectarse a los productos de Azure SQL que se enumeraron al principio de este artículo. No es compatible con SQL Server (ni local ni en una máquina virtual).
- *Autenticación interactiva de Active Directory* no se admite en el cuadro de diálogo de conexión en el *Explorador de servidores*. Debe conectarse mediante SSDT con el *Explorador de objetos de SQL Server*.
- La integración del inicio de sesión único con la cuenta de Visual Studio que inició la sesión no es compatible con SSDT.
- El archivo SQLPackage.exe que se instaló en el directorio de extensiones durante la instalación de Visual Studio no está pensado para usarlo desde esa ubicación. Para usar SQLPackage.exe con Azure AD, vaya a [https://www.microsoft.com/download/details.aspx?id=55088](https://www.microsoft.com/download/details.aspx?id=55088). 
- No se admite la comparación de datos de SSDT para la autenticación de Azure AD.  


## <a name="see-also"></a>Consulte también  

[Autenticación multifactor](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication)  
[Autenticación de Azure Active Directory con SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication-configure)  
[Foro MSDN de SSDT](https://social.msdn.microsoft.com/Forums/sqlserver/home?forum=ssdt)  
[Blog del equipo de SSDT](https://blogs.msdn.com/b/ssdt/)  
[Referencia de la API de DACFx](https://msdn.microsoft.com/library/dn645454.aspx)  
[Descarga de SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)  
