---
title: Conectar al servidor (Integration Services) | Microsoft Docs
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
- sql13.swb.connection.login.dtsserver.f1
ms.assetid: 5be897bd-f36c-4c6a-a91a-13d0d016f8b6
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4d7f292d113fb3d9bc8197f7be3134524e8116af
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-integration-services"></a>Conectar al servidor (Integration Services)
Use este cuadro de diálogo para ver o especificar opciones cuando se conecte a [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)].  
  
## <a name="options"></a>Opciones  
**Tipo de servidor**  
Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que conectarse: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro Tipo de servidor es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo distinto de servidor, seleccione [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services desde la barra de herramientas Servidores registrados antes de comenzar a registrar un servidor nuevo.  
  
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
  
**Connect**  
Haga clic aquí para conectarse al servidor seleccionado anteriormente.  
  
**Opciones**  
Haga clic aquí para que se muestren las opciones adicionales de conexión al servidor, como registrar un servidor y recordar la contraseña.  
  

