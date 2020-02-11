---
title: Nuevo o editar el registro de servidor (pestaña general) (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerserver.general.reportserver.f1
ms.assetid: 5f899a8e-52ef-46b5-b7a9-f200ccd9f724
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0e6d6d3ad57726c42556c9ecc2662edce102e57
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62844281"
---
# <a name="new-or-edit-server-registration-general-tab-reporting-services"></a>Nuevo o Editar propiedades de registro de servidor (pestaña General de Reporting Services)
  Utilice esta pestaña para especificar opciones cuando registre una instancia de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Para obtener acceso a esta página, en Servidores registrados, haga clic en **Reporting Services** , en la barra de herramientas de **Servidores registrados** haga clic con el botón derecho en cualquier grupo de servidores registrados como, por ejemplo, **Reporting Services**, seleccione **Nuevo**y haga clic en **Registro de servidor**.  
  
## <a name="options"></a>Opciones  
 **Tipo de servidor**  
 Cuando se registra un servidor desde servidores registrados, el cuadro **tipo de servidor** es de solo lectura y coincide con el tipo de servidor que se muestra en el panel **servidores registrados** . Para registrar un tipo de servidor diferente, haga clic en el servidor que desee en la barra de herramientas de **Servidores registrados** antes de comenzar a registrar un nuevo servidor.  
  
 **Nombre del servidor**  
 Especifique la instancia de servidor de informes a la que se va a conectar. En [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], puede tener acceso al servidor de informes a través de su nombre de instancia. Puede tener una instancia de servidor de informes para cada instancia de SQL Server que instale. Si utiliza la instancia predeterminada, escriba el nombre de la instancia de SQL Server. Si utiliza una instancia con nombre, especifique la instancia con nombre para conectar al servidor de informes en el formato MSSQL$InstanceName.  
  
 **Autenticación**  
 La autenticación del servidor de informes se realiza a través de Internet Information Services (IIS). Seleccione uno de los siguientes modos de autenticación al conectarse a Reporting Services:  
  
 **Modo de autenticación de Windows (autenticación de Windows)**  
 Se conecta a una instancia de servidor de informes usando sus credenciales de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows.  
  
 **Autenticación básica**  
 Conéctese mediante la **Autenticación básica** si la instalación de Reporting Services está configurada para usar la Autenticación básica.  
  
 **Autenticación mediante formularios**  
 Conéctese mediante la **Autenticación de formularios** si la instalación de Reporting Services está configurada para usar una extensión de autenticación personalizada.  
  
 **Nombre de usuario**  
 Escriba el nombre de inicio de sesión que se va a usar en la conexión. Esta opción solo se encuentra disponible si ha seleccionado **Autenticación básica** o **Autenticación de formularios**.  
  
 **Contraseña**  
 Escriba la contraseña del nombre de usuario Esta opción solo se puede editar si ha seleccionado **Autenticación básica** o **Autenticación de formularios**.  
  
 **Recordar contraseña**  
 Guarda la contraseña que ha escrito. Esta opción solo se encuentra disponible si ha seleccionado **Autenticación básica** o **Autenticación de formularios**.  
  
> [!NOTE]  
>  Si ha almacenado la contraseña y desea dejar de almacenarla, desactive esta casilla y, a continuación, haga clic en **Guardar**.  
  
 **Nombre del servidor registrado**  
 El nombre que desea que aparezca en Servidores registrados. Este nombre no tiene que coincidir con el cuadro **Nombre del servidor** .  
  
 **Descripción del servidor registrado**  
 Escriba una descripción opcional del servidor.  
  
 **Muestre**  
 Haga clic para probar la conexión al servidor seleccionado en **Nombre del servidor**.  
  
 **Guardar**  
 Haga clic aquí para guardar la configuración del servidor registrado.  
  
  
