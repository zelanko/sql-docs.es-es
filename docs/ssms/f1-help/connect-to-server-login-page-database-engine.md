---
title: "Conectar al servidor (página Inicio de sesión del motor de base de datos) | Microsoft Docs"
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
- sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1556c7facc4a671767fe2d6c061b4f6655ba521b
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-login-page-database-engine"></a>Conectar al servidor (página Inicio de sesión del motor de base de datos)
Use esta pestaña para ver o especificar opciones cuando se conecte a [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)].  
  
> [!NOTE]  
> Para conectarse utilizando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , es necesario configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en el modo de autenticación de Windows y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Para más información sobre cómo determinar el modo de autenticación y cambiarlo, consulte [Cambiar el modo de autenticación del servidor](http://msdn.microsoft.com/en-us/79babcf8-19fd-4495-b8eb-453dc575cac0).  
  
## <a name="options"></a>Opciones  
**Tipo de servidor**  
Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que conectarse: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro **Tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo distinto de servidor, seleccione [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services desde la barra de herramientas Servidores registrados antes de comenzar a registrar un servidor nuevo.  
  
Al conectarse a una instancia del motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a través de la base de datos de [!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)], es preciso que use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y especifique una base de datos en el cuadro de diálogo **Conectar al servidor** en la pestaña **Propiedades de conexión** . Asegúrese de que activa la casilla **Cifrar conexión** .  
  
De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se conecta a **master**. Si especifica una base de datos de usuario, verá solo esa base de datos y sus objetos en el Explorador de objetos. Si se conecta a **master**, podrá ver todas las bases de datos. Para más información, consulte la [Introducción a Microsoft Azure SQL Database](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
**Nombre del servidor**  
Seleccione la instancia de servidor a la que va a conectarse. De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
**Autenticación**  
Están disponibles dos modos de autenticación cuando se conecta a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)].  
  
Al conectarse a una instancia del motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a través de la base de datos de [!INCLUDE[ssSDS](../../includes/sssds_md.md)], es preciso que use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y especifique una base de datos en el cuadro de diálogo **Conectar al servidor** en la pestaña **Propiedades de conexión** . Asegúrese de que activa la casilla **Cifrar conexión** .  
  
De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se conecta a **master**. Si especifica una base de datos de usuario, verá solo esa base de datos y sus objetos en el Explorador de objetos. Si se conecta a **master**, podrá ver todas las bases de datos. Para más información, consulte la [Introducción a Microsoft Azure SQL Database](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
**Autenticación de Windows**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] El modo de autenticación de Windows permite al usuario conectarse mediante una cuenta de usuario de Windows.  
  
**Autenticación de SQL Server**  
Cuando un usuario se conecta con un nombre y una contraseña de inicio de sesión determinados desde una conexión no confiable, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] realiza la autenticación y comprueba si se configuró una cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y si la contraseña especificada coincide con la almacenada anteriormente. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no tiene configurada una cuenta de inicio de sesión, la autenticación no se realizará correctamente y el usuario recibirá un mensaje de error.  
  
> [!IMPORTANT]  
> Siempre que sea posible, utilice la autenticación de Windows.  
  
**Autenticación universal de Active Directory**  
Autenticación universal de Active Directory es un flujo de trabajo interactivo que es compatible con Azure Multi-Factor Authentication (MFA). Azure MFA ayuda a proteger el acceso a los datos y las aplicaciones mientras se cumple la exigencia del usuario en cuanto a un proceso de inicio de sesión simple. Ofrece una autenticación segura con una variedad de opciones de comprobación sencillas, como llamadas de teléfono, mensajes de texto, tarjetas inteligentes con PIN o notificaciones de aplicaciones móviles, que permiten que los usuarios elijan el método de su preferencia. Si la cuenta de usuario está configurada para MFA, el flujo de trabajo de autenticación interactivo requiere una interacción adicional por parte del usuario a través de cuadros de diálogo emergentes, las tarjetas inteligentes, etc. Si la cuenta de usuario está configurada para MFA, el usuario debe seleccionar Autenticación universal de Azure para conectarse. Si la cuenta de usuario no requiere MFA, el usuario puede usar de todas maneras las otras dos opciones de Autenticación de Azure Active Directory. Para más información, consulte [Compatibilidad de SSMS con Azure AD MFA con SQL Database y SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Requiere al menos la versión 16.3 de SSMS (agosto de 2016).
  
**Autenticación de contraseña de Active Directory**  
Autenticación de Azure Active Directory es un mecanismo que permite conectar con [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] mediante identidades de Azure Active Directory.  Use este método para conectarse con [!INCLUDE[ssSDS](../../includes/sssds_md.md)] si inició sesión en Windows con credenciales de un dominio no federado con Azure o si usa la autenticación de Azure AD con Azure AD basado en el dominio inicial o de cliente. Para más información, consulte [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Autenticación integrada de Active Directory**  
Autenticación de Azure Active Directory es un mecanismo que permite conectar con [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] mediante identidades de Azure Active Directory. Use este método para conectarse con [!INCLUDE[ssSDS](../../includes/sssds_md.md)] si inició sesión en Windows con credenciales de Azure Active Directory de un dominio federado. Para más información, consulte [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**Nombre de usuario.**  
El nombre de usuario de Windows con el que se va a conectar. Esta opción solo está disponible si seleccionó **Autenticación de contraseña de Active Directory**para conectarse. Si selecciona **Autenticación de Windows**, esta opción es de solo lectura.  
  
**Inicio de sesión**  
Escriba el inicio de sesión con el que va a conectarse. Esta opción solo está disponible si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para conectarse.  
  
**Contraseña**  
Escriba la contraseña del inicio de sesión. Esta opción solo es editable si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para conectarse.  
  
**Recordar contraseña**  
Haga clic aquí para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] guarde la contraseña que ha escrito. Esta opción solo aparece si seleccionó Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para conectarse.  
  
**Connect**  
Haga clic aquí para conectarse al servidor seleccionado anteriormente.  
  
**Opciones**  
Haga clic aquí para modificar el cuadro de diálogo y ocultar las opciones adicionales de conexión al servidor, como recordar la contraseña.  
  

