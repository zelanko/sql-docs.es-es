---
title: Conectar al servidor (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connection.login.dtsserver.f1
ms.assetid: 5be897bd-f36c-4c6a-a91a-13d0d016f8b6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64c565c45288de157a3ba4c6c367ae7f8849dfee
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096265"
---
# <a name="connect-to-server-integration-services"></a>Conectar al servidor (Integration Services)
  Use este cuadro de diálogo para ver o especificar opciones cuando se conecte a [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
 **Tipo de servidor**  
 Al registrar un servidor desde el Explorador de objetos, seleccione el tipo de servidor al que conectarse: [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services. El resto del cuadro de diálogo muestra simplemente las opciones que se aplican al tipo de servidor seleccionado. Cuando se registra un servidor desde Servidores registrados, el cuadro Tipo de servidor es de solo lectura y coincide con el tipo de servidor que se muestra en el componente Servidores registrados. Para registrar un tipo distinto de servidor, seleccione [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services o Integration Services desde la barra de herramientas Servidores registrados antes de comenzar a registrar un servidor nuevo.  
  
 **Nombre del servidor**  
 Seleccione el servidor al que va a conectarse. De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
> [!NOTE]  
>  No use  *\<servername >*\\*\<instancename >*, ya que [!INCLUDE[ssIS](../includes/ssis-md.md)] no admite varias instancias en un equipo.  
  
 **Autenticación**  
 La autenticación [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows solo está disponible para [!INCLUDE[ssIS](../includes/ssis-md.md)]. Windows permite al usuario conectarse mediante una cuenta de usuario de Windows.  
  
 **Nombre de usuario.**  
 Esta opción no está disponible ya que la autenticación de Windows solo está disponible para [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
 **Contraseña**  
 Esta opción no está disponible ya que la autenticación de Windows solo está disponible para [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
 **Conectar**  
 Haga clic aquí para conectarse al servidor seleccionado anteriormente.  
  
 **Opciones**  
 Haga clic aquí para que se muestren las opciones adicionales de conexión al servidor, como registrar un servidor y recordar la contraseña.  
  
  
