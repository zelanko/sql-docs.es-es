---
title: "Conectar al servidor (página Inicio de sesión del motor de base de datos) | Microsoft Docs"
ms.custom: 
ms.date: 08/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-f1
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: "6"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6f3824ace141704fb08b29ddbf08890d5299f494
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="connect-to-server-login-page-database-engine"></a>Conectar al servidor (página Inicio de sesión del motor de base de datos)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Use esta pestaña para ver o especificar opciones cuando se conecte a [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]. En la mayoría de los casos, para conectarse, puede escribir el nombre del servidor de base de datos en el cuadro **Nombre del servidor** y hacer clic en **Conectar**. Si se está conectando con una instancia con nombre, use el nombre del equipo seguido de una barra inversa y, después, el nombre de la instancia. Por ejemplo, `mycomputer\myinstance`. Si se está conectando a [!INCLUDE[ssExpress](../../includes/ssexpress_md.md)], use el nombre del equipo seguido de **\sqlexpress**.  
  
Hay diversos factores que pueden afectar a la capacidad de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener ayuda, vea los recursos siguientes:  
- [Lección 1 del tutorial: Conexión al motor de base de datos](../../relational-databases/lesson-1-connecting-to-the-database-engine.md)  
- [Solucionar problemas de conexión al motor de base de datos de SQL Server](../../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md)  
- [Resolver errores de conectividad en SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server)    
  
> [!NOTE]  
> Para conectarse utilizando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , es necesario configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en el modo de autenticación de Windows y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Para más información sobre cómo determinar el modo de autenticación y cambiarlo, consulte [Cambiar el modo de autenticación del servidor](http://msdn.microsoft.com/en-us/79babcf8-19fd-4495-b8eb-453dc575cac0).  
  
## <a name="options"></a>.  
**Tipo de servidor**  
Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que conectarse: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro **Tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo distinto de servidor, seleccione [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services desde la barra de herramientas Servidores registrados antes de comenzar a registrar un servidor nuevo.  
  
Al conectarse a una instancia del motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a través de la base de datos de [!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)], es preciso que use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y especifique una base de datos en el cuadro de diálogo **Conectar al servidor** en la pestaña **Propiedades de conexión** . Asegúrese de que activa la casilla **Cifrar conexión** .  
  
De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se conecta a **master**. Si especifica una base de datos de usuario, verá solo esa base de datos y sus objetos en el Explorador de objetos. Si se conecta a **master**, podrá ver todas las bases de datos. Para más información, consulte la [Introducción a Microsoft Azure SQL Database](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
**Nombre del servidor**  
Seleccione la instancia de servidor a la que va a conectarse. De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
**Autenticación**  
La versión actual de SSMS ofrece cinco modos de autenticación al conectarse a una instancia del [!INCLUDE[ssDE](../../includes/ssde_md.md)]. Si el cuadro de diálogo de autenticación no coincide con la lista siguiente, descargue la versión más reciente de SSMS desde [Descarga de SQL Server Management Studio (SSMS)](../download-sql-server-management-studio-ssms.md).     
  
Al conectarse a una instancia del motor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] a través de la base de datos de [!INCLUDE[ssSDS](../../includes/sssds_md.md)], es preciso que use la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y especifique una base de datos en el cuadro de diálogo **Conectar al servidor** en la pestaña **Propiedades de conexión** . Asegúrese de que activa la casilla **Cifrar conexión** .  
  
De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] se conecta a **master**. Si especifica una base de datos de usuario al conectarse a [!INCLUDE[ssSDS](../../includes/sssds_md.md)], verá solo esa base de datos y sus objetos en el Explorador de objetos. Si se conecta a **master**, podrá ver todas las bases de datos. Para más información, consulte la [Introducción a Microsoft Azure SQL Database](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
  > **Autenticación de Windows**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] El modo de autenticación de Windows permite al usuario conectarse mediante una cuenta de usuario de Windows.  
  
  > **Autenticación de SQL Server**  
Cuando un usuario se conecta con un nombre y una contraseña de inicio de sesión determinados desde una conexión no confiable, [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] realiza la autenticación y comprueba si se configuró una cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y si la contraseña especificada coincide con la almacenada anteriormente. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no tiene configurada una cuenta de inicio de sesión, la autenticación no se realizará correctamente y el usuario recibirá un mensaje de error. Siempre que sea posible, utilice la autenticación de Windows.  
  
  > **Active Directory - Universal compatible con MFA**  
Active Directory - Universal compatible con MFA es un flujo de trabajo interactivo que es compatible con Azure Multi-Factor Authentication (MFA). Azure MFA ayuda a proteger el acceso a los datos y las aplicaciones mientras se cumple la exigencia del usuario en cuanto a un proceso de inicio de sesión simple. Ofrece una autenticación segura con una variedad de opciones de comprobación sencillas, como llamadas de teléfono, mensajes de texto, tarjetas inteligentes con PIN o notificaciones de aplicaciones móviles, que permiten que los usuarios elijan el método de su preferencia. Si la cuenta de usuario está configurada para MFA, el flujo de trabajo de autenticación interactivo requiere una interacción adicional por parte del usuario a través de cuadros de diálogo emergentes, las tarjetas inteligentes, etc. Si la cuenta de usuario está configurada para MFA, el usuario debe seleccionar Autenticación universal de Azure para conectarse. Si la cuenta de usuario no requiere MFA, el usuario puede usar de todas maneras las otras dos opciones de Autenticación de Azure Active Directory. Para más información, consulte [Compatibilidad de SSMS con Azure AD MFA con SQL Database y SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/). Si es necesario, puede cambiar el dominio que autentica el inicio de sesión. Para ello, haga clic en **Opciones**, seleccione la pestaña **Propiedades de conexión** y complete el cuadro **Nombre de dominio o ID de inquilino de AD**.  

  > **Active Directory - Contraseña**  
Autenticación de Azure Active Directory es un mecanismo que permite conectar con [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] mediante identidades de Azure Active Directory.  Use este método para conectarse con [!INCLUDE[ssSDS](../../includes/sssds_md.md)] si ha iniciado sesión en Windows con credenciales de un dominio no federado con Azure o si usa la autenticación de Azure AD con Azure AD basado en el dominio inicial o de cliente. Para más información, consulte [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
  > **Active Directory - Integrado**  
Autenticación de Azure Active Directory es un mecanismo que permite conectar con [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssSDSfull](../../includes/sssdsfull_md.md)] mediante identidades de Azure Active Directory. Use este método para conectarse con [!INCLUDE[ssSDS](../../includes/sssds_md.md)] si ha iniciado sesión en Windows con credenciales de Azure Active Directory de un dominio federado. Para más información, consulte [Conexión a Base de datos SQL mediante autenticación de Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/).  
  
**User name**  
El nombre de usuario de Windows con el que se va a conectar. Esta opción solo está disponible si seleccionó **Autenticación de contraseña de Active Directory**para conectarse. Es de solo lectura cuando se selecciona **Autenticación de Windows** o la autenticación **Active Directory - Integrado**.  
  
**Inicio de sesión**  
Escriba el inicio de sesión con el que va a conectarse. Esta opción solo está disponible si se ha seleccionado Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Autenticación de contraseña de Active Directory para conectarse.  
  
**Contraseña**  
Escriba la contraseña del inicio de sesión. Esta opción solo se puede editar si se ha seleccionado Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o Autenticación de contraseña de Active Directory para conectarse.  
  
**Recordar contraseña**  
Haga clic aquí para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] guarde la contraseña que ha escrito. Esta opción solo aparece si seleccionó Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para conectarse.  
  
**Conectar**  
Haga clic para conectar con el servidor.  
  
**Opciones**  
Haga clic para mostrar las pestañas **Propiedades de conexión** y **Parámetros de conexión adicionales**.  
   
  
