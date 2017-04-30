---
title: "Conectar con el servidor (página Inicio de sesión de Integration Services) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connecttodts.login.f1
- sql13.swb.connecttodtsserver.login.f1
ms.assetid: 402c2de4-f4ea-40b0-909f-3ddf3bd59950
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 18699131b8268dedfb0e47f05ec4032d81b498ef
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-login-page-integration-services"></a>Conectar al servidor (página Inicio de sesión de Integration Services)
Use esta pestaña para ver o especificar las siguientes opciones cuando se conecte a [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)].  
  
## <a name="options"></a>Opciones  
**Tipo de servidor**  
Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que conectarse: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro **Tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo distinto de servidor, seleccione [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services desde la barra de herramientas Servidores registrados antes de comenzar a registrar un servidor nuevo.  
  
**Nombre del servidor**  
Seleccione el servidor al que va a conectarse. De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
> [!NOTE]  
> No use *<servername>*\\*<instancename>*, porque [!INCLUDE[ssIS](../../includes/ssis_md.md)] no admite varias instancias en un equipo.  
  
**Autenticación**  
La autenticación [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows solo está disponible para [!INCLUDE[ssIS](../../includes/ssis_md.md)]. El modo de autenticación de Windows permite al usuario conectarse mediante una cuenta de usuario de Windows.  
  
**Nombre de usuario.**  
Esta opción no está disponible ya que la autenticación de Windows solo está disponible para [!INCLUDE[ssIS](../../includes/ssis_md.md)].  
  
**Contraseña**  
Esta opción no está disponible ya que la autenticación de Windows solo está disponible para [!INCLUDE[ssIS](../../includes/ssis_md.md)].  
  
**Recordar contraseña**  
Esta opción no está disponible ya que la autenticación de Windows solo está disponible para [!INCLUDE[ssIS](../../includes/ssis_md.md)].  
  
**Connect**  
Se conecta al servidor seleccionado anteriormente.  
  
**Opciones**  
Haga clic aquí para modificar el cuadro de diálogo y ocultar las opciones adicionales de conexión al servidor, como recordar la contraseña.  
  

