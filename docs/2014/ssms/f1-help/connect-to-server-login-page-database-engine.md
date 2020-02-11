---
title: Conectar al servidor (página Inicio de sesión del motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2fe246a1f8baf1ab9f60ab1fa73e21e81c052aa1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "70153703"
---
# <a name="connect-to-server-login-page-database-engine"></a>Conectar al servidor (página Inicio de sesión del motor de base de datos)
  Use esta pestaña para ver o especificar opciones cuando se conecte [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]a.  
  
> [!NOTE]  
>  Para conectarse utilizando la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , es necesario configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el modo de autenticación de Windows y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información sobre cómo determinar el modo de autenticación y cambiar el modo de autenticación, consulte [cambiar el modo de autenticación del servidor](../../database-engine/configure-windows/change-server-authentication-mode.md).  
  
## <a name="options"></a>Opciones  
 **Tipo de servidor**  
 Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que conectarse: [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro **Tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo distinto de servidor, seleccione [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services desde la barra de herramientas Servidores registrados antes de comenzar a registrar un servidor nuevo.  
  
 Al conectarse a una instancia de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos a [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]través de, debe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar la autenticación de y especificar una base de datos en el cuadro de diálogo **conectar al servidor** , en la pestaña **propiedades de conexión** . Asegúrese de activar la casilla **cifrar conexión** .  
  
 De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a **master**. Si especifica una base de datos de usuario, verá solo esa base de datos y sus objetos en el Explorador de objetos. Si se conecta a **master**, podrá ver todas las bases de datos. Para obtener más información, vea la información [General de Azure SQL Database](/azure/sql-database/sql-database-technical-overview).  
  
 **Nombre del servidor**  
 Seleccione la instancia de servidor a la que va a conectarse. De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
 **Autenticación**  
 Están disponibles dos modos de autenticación cuando se conecta a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Al conectarse a una instancia de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] motor de base de datos a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]través de, debe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar la autenticación de y especificar una base de datos en el cuadro de diálogo **conectar al servidor** , en la pestaña **propiedades de conexión** . Asegúrese de activar la casilla **cifrar conexión** .  
  
 De forma predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a **master**. Si especifica una base de datos de usuario, verá solo esa base de datos y sus objetos en el Explorador de objetos. Si se conecta a **master**, podrá ver todas las bases de datos. Para obtener más información, vea la información [General de Azure SQL Database](/azure/sql-database/sql-database-technical-overview).  
  
 **Modo de autenticación de Windows (autenticación de Windows)**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)]El modo de autenticación de Windows permite a un usuario conectarse a través de una cuenta de usuario de Windows.  
  
 **Autenticación de SQL Server**  
 Cuando un usuario se conecta con un nombre y una contraseña de inicio de sesión determinados desde una conexión no confiable, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza la autenticación y comprueba si se configuró una cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y si la contraseña especificada coincide con la almacenada anteriormente. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no tiene configurada una cuenta de inicio de sesión, la autenticación no se realizará correctamente y el usuario recibirá un mensaje de error.  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows.  
  
 **Nombre de usuario**  
 Escriba el nombre de usuario con el que se va a conectar. Esta opción solo está disponible si ha seleccionado la autenticación de Windows para conectarse.  
  
 **Inicio de sesión**  
 Escriba el inicio de sesión con el que va a conectarse. Esta opción solo está disponible si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse.  
  
 **Contraseña**  
 Escriba la contraseña del inicio de sesión. Esta opción solo es editable si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse.  
  
 **Recordar contraseña**  
 Haga clic aquí para que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] guarde la contraseña que ha escrito. Esta opción solo aparece si seleccionó Autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse.  
  
 **Conectar**  
 Haga clic aquí para conectarse al servidor seleccionado anteriormente.  
  
 **Opciones**  
 Haga clic aquí para modificar el cuadro de diálogo y ocultar las opciones adicionales de conexión al servidor, como recordar la contraseña.  
  
  
