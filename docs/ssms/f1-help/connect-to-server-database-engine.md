---
title: Conectar al servidor (motor de base de datos) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connectoserverunknownservertype.f1
- sql13.swb.connection.login.sqlce.f1
- sql13.swb.connecttoce.f1
- SQL13.SWB.CONNECTION.LOGIN.SQLSERVER.F1
- sql13.swb.connection.login.sqlserver.f1
- sql13.swb.manageSS2k.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d421bcb09ec7ebde28b5d1cce6eca2263cfb1c48
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-database-engine"></a>Conectar al servidor (motor de base de datos)
Utilice este cuadro de diálogo para ver o especificar opciones cuando se conecte a [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]. En la mayoría de los casos, para conectarse, puede escribir el nombre del servidor de base de datos en el cuadro **Nombre del servidor** y hacer clic en **Conectar**. Si se está conectando a [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], use el nombre del equipo seguido de **\sqlexpress**.  
  
Hay diversos factores que pueden afectar a la capacidad de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
## <a name="options"></a>Opciones  
**Tipo de servidor**  
Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que se conectará: [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)]o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)]. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro **Tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo de servidor distinto, seleccione [!INCLUDE[ssDE](../../includes/ssde_md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion_md.md)], [!INCLUDE[ssEW](../../includes/ssew_md.md)]o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)] desde la barra de herramientas Servidores registrados antes de comenzar a registrar un nuevo servidor.  
  
**Nombre del servidor**  
Seleccione la instancia de servidor a la que va a conectarse. De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
> [!NOTE]  
> Para conectarse a una instancia de usuarios activos de [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] , use el protocolo Canalizaciones con nombre especificando el nombre de canalización, como np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query. Para más información, consulte la documentación de [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)] .  
  
**Autenticación**  
Dispone de tres modos de autenticación al conectarse a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
**Autenticación de Windows**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] El modo de autenticación de Windows permite al usuario conectarse mediante una cuenta de usuario de Windows.  
  
**Autenticación de SQL Server**  
Cuando un usuario se conecta con un nombre y una contraseña de inicio de sesión determinados desde una conexión no confiable, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] realiza la autenticación y comprueba si se configuró una cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y si la contraseña especificada coincide con la almacenada anteriormente. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no tiene configurada una cuenta de inicio de sesión, la autenticación no se realizará correctamente y el usuario recibirá un mensaje de error.  
  
> [!IMPORTANT]  
> Siempre que sea posible, use la autenticación de Windows o Autenticación de contraseña de Active Directory.  
  
**Autenticación universal de Active Directory**  
Autenticación universal de Active Directory es un flujo de trabajo interactivo que es compatible con Azure Multi-Factor Authentication (MFA). Azure MFA ayuda a proteger el acceso a los datos y las aplicaciones mientras se cumple la exigencia del usuario en cuanto a un proceso de inicio de sesión simple. Ofrece una autenticación segura con una variedad de opciones de comprobación sencillas, como llamadas de teléfono, mensajes de texto, tarjetas inteligentes con PIN o notificaciones de aplicaciones móviles, que permiten que los usuarios elijan el método de su preferencia. Si la cuenta de usuario está configurada para MFA, el flujo de trabajo de autenticación interactivo requiere una interacción adicional por parte del usuario a través de cuadros de diálogo emergentes, las tarjetas inteligentes, etc. Si la cuenta de usuario está configurada para MFA, el usuario debe seleccionar Autenticación universal de Azure para conectarse. Si la cuenta de usuario no requiere MFA, el usuario puede usar de todas maneras las otras dos opciones de Autenticación de Azure Active Directory. Para más información, consulte [Compatibilidad de SSMS con Azure AD MFA con SQL Database y SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Requiere al menos la versión 16.3 de SSMS (agosto de 2016).

**Autenticación de contraseña de Active Directory**  
Autenticación de Azure Active Directory es un mecanismo que permite conectar con [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] mediante identidades de Azure Active Directory.  Use este método para conectarse con [!INCLUDE[ssSDS](../../includes/sssds_md.md)] si inició sesión en Windows con credenciales de un dominio no federado con Azure o si usa la autenticación de Azure AD con Azure AD basado en el dominio inicial o de cliente. Para más información, consulte [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Autenticación integrada de Active Directory**  
Autenticación de Azure Active Directory es un mecanismo que permite conectar con [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] mediante identidades de Azure Active Directory. Use este método para conectarse con [!INCLUDE[ssSDS](../../includes/sssds_md.md)] si inició sesión en Windows con credenciales de Azure Active Directory de un dominio federado. Para más información, consulte [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Nombre de usuario.**  
El nombre de usuario de Windows con el que se va a conectar. Esta opción solo está disponible si seleccionó **Autenticación de contraseña de Active Directory**para conectarse. Si selecciona **Autenticación de Windows**, esta opción es de solo lectura.  
  
**Inicio de sesión**  
Escriba el inicio de sesión con el que va a conectarse. Esta opción solo está disponible si seleccionó la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Autenticación de contraseña de Active Directory para conectarse.  
  
**Contraseña**  
Escriba la contraseña del inicio de sesión. Esta opción solo se puede editar si seleccionó la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Autenticación de contraseña de Active Directory para conectarse.  
  
**Conectar**  
Haga clic aquí para conectarse al servidor seleccionado anteriormente.  
  
**Opciones**  
Haga clic aquí para que se muestren las opciones adicionales de conexión al servidor, como registrar un servidor y recordar la contraseña.  
  

