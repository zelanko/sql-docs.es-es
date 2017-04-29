---
title: Conectar al servidor (Analysis Services) | Microsoft Docs
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
- sql13.swb.connection.login.analysisserver.f1
ms.assetid: 7e277d22-8d4b-422e-8882-7c5dd7a6d915
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 73451189bc401a4167c65261f3adcc5aabb6627c
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-analysis-services"></a>Conectar al servidor (Analysis Services)
Use este cuadro de diálogo para ver o especificar opciones cuando se conecte a [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)].  
  
## <a name="options"></a>Opciones  
**Tipo de servidor**  
Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que conectarse: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro **Tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo distinto de servidor, seleccione [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services o Integration Services desde la barra de herramientas Servidores registrados antes de comenzar a registrar un servidor nuevo.  
  
**Nombre del servidor**  
Seleccione la instancia de servidor a la que va a conectarse. De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
**Autenticación**  
Cuando se conecta a una instancia de Analysis Services, se admiten los siguientes modos de autenticación: autenticación de [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows.  
  
**Modo de autenticación de Windows (autenticación de Windows)**  
El modo de**autenticación de Windows** permite al usuario conectarse mediante una cuenta de usuario de Windows.  
  
**Nombre de usuario.**  
Esta opción no está disponible en esta versión. Escriba el nombre de usuario con el que se va a conectar. Esta opción solo está disponible si ha seleccionado la **autenticación de Windows**para conectarse.  
  
**Contraseña**  
Esta opción no está disponible en esta versión. Escriba la contraseña del inicio de sesión. Esta opción solo es editable si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para conectarse.  
  
**Connect**  
Haga clic aquí para conectarse al servidor seleccionado anteriormente.  
  
**Opciones**  
Haga clic aquí para que se muestren las opciones adicionales de conexión al servidor, como registrar un servidor y recordar la contraseña.  
  

