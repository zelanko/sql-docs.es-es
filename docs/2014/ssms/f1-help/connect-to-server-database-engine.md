---
title: Conectar al servidor (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connectoserverunknownservertype.f1
- sql12.swb.connection.login.sqlserver.f1
- sql12.swb.connection.login.sqlce.f1
- sql12.swb.manageSS2k.f1
- sql12.swb.connecttoce.f1
- sql12.swb.connecttoce.connectionproperties.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 50a593c625fe50e5d7a1dfbebc40222ac13433c2
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43808281"
---
# <a name="connect-to-server-database-engine"></a>Conectar al servidor (motor de base de datos)
  Use este cuadro de diálogo para ver o especificar opciones cuando se conecte a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. En la mayoría de los casos, para conectarse, puede escribir el nombre del servidor de base de datos en el cuadro **Nombre del servidor** y hacer clic en **Conectar**. Si se está conectando a [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], use el nombre del equipo seguido de **\sqlexpress**.  
  
 Hay diversos factores que pueden afectar a la capacidad de conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
 **Tipo de servidor**  
 Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que se conectará: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro **Tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo de servidor distinto, seleccione [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssEW](../../includes/ssew-md.md)]o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] desde la barra de herramientas Servidores registrados antes de comenzar a registrar un nuevo servidor.  
  
 **Nombre del servidor**  
 Seleccione la instancia de servidor a la que va a conectarse. De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
> [!NOTE]  
>  Para conectarse a una instancia de usuarios activos de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , use el protocolo Canalizaciones con nombre especificando el nombre de canalización, como np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query. Para más información, consulte la documentación de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] .  
  
 **Autenticación**  
 Dispone de dos modos de autenticación al conectarse a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 **Modo de autenticación de Windows (autenticación de Windows)**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] El modo de autenticación de Windows permite al usuario conectarse mediante una cuenta de usuario de Windows.  
  
 **Autenticación de SQL Server**  
 Cuando un usuario se conecta con un nombre y una contraseña de inicio de sesión determinados desde una conexión no confiable, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza la autenticación y comprueba si se configuró una cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y si la contraseña especificada coincide con la almacenada anteriormente. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no tiene configurada una cuenta de inicio de sesión, la autenticación no se realizará correctamente y el usuario recibirá un mensaje de error.  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows.  
  
 **Nombre de usuario.**  
 Escriba el nombre de usuario con el que se va a conectar. Esta opción solo está disponible si ha seleccionado la autenticación de Windows para conectarse.  
  
 **Inicio de sesión**  
 Escriba el inicio de sesión con el que va a conectarse. Esta opción solo está disponible si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse.  
  
 **Contraseña**  
 Escriba la contraseña del inicio de sesión. Esta opción solo es editable si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse.  
  
 **Conectar**  
 Haga clic aquí para conectarse al servidor seleccionado anteriormente.  
  
 **Opciones**  
 Haga clic aquí para que se muestren las opciones adicionales de conexión al servidor, como registrar un servidor y recordar la contraseña.  
  
  
