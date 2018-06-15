---
title: Seleccionar origen (cuadro de diálogo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.selectsource.f1
ms.assetid: d664c2e5-dd0c-4da8-b27d-aa4ee4fc0ffd
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f5138982829e14779632ddbb60aad34c63ac1b54
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32955390"
---
# <a name="select-source-dialog-box"></a>Seleccionar origen (cuadro de diálogo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice este cuadro de diálogo para seleccionar el origen de las directivas que se van a ejecutar. Para seleccionar uno o más archivos XML que contienen directivas, seleccione **Archivos**. Para ejecutar las directivas que se buscan en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione **Servidor**.  
  
 Puede abrir este cuadro de diálogo de varias maneras.  
  
 **Para abrir este cuadro de diálogo**  
  
-   En Servidores registrados, haga clic con el botón derecho en **Grupos de servidores locales** , en cualquier servidor de **Grupos de servidores locales**o en cualquier servidor de **Servidores de administración central**y seleccione **Evaluar directivas**. En la página **Selección de directiva** del cuadro de diálogo **Evaluar directivas** , haga clic en el botón Examinar (**...**).  
  
-   En el Explorador de objetos, expanda **Administración**, expanda **Administración de directivas**, haga clic con el botón derecho en **Directivas**y, después, seleccione **Importar directiva**. En el cuadro de diálogo **Importar** , haga clic en el botón Examinar (**...**).  
  
-   En el Explorador de objetos, haga clic con el botón derecho en un servidor, una base de datos o un objeto de base de datos, seleccione **Directivas**y, después, seleccione **Evaluar**. En la página **Selección de directiva** del cuadro de diálogo **Evaluar directivas** , haga clic en el botón Examinar (**...**).  
  
## <a name="options"></a>Opciones  
 **Archivos**  
 Seleccione uno o más archivos XML que contienen directivas.  
  
 **Servidor**  
 Permite seleccionar un servidor que contiene las directivas que se desean ejecutar.  
  
 **Tipo de servidor**  
 Solo los servidores de [!INCLUDE[ssDE](../../includes/ssde-md.md)] contienen directivas. Este cuadro es de solo lectura.  
  
 **Nombre del servidor**  
 Seleccione la instancia de servidor a la que va a conectarse. De forma predeterminada, aparecerá la instancia de servidor a la que se ha conectado por última vez.  
  
 **Autenticación**  
 Dispone de dos modos de autenticación cuando se conecta a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 **Modo de autenticación de Windows (autenticación de Windows)**  
 El modo de autenticación de Windows permite que un usuario pueda conectarse a través de una cuenta de usuario de Windows.  
  
 **Autenticación de SQL Server**  
 Cuando un usuario se conecta con un nombre y una contraseña de inicio de sesión específicos desde una conexión que no es de confianza, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza la autenticación y comprueba si se ha configurado una cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y si la contraseña especificada coincide con la que se ha almacenado anteriormente. Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no tiene configurada una cuenta de inicio de sesión, la autenticación no se realizará correctamente y el usuario recibirá un mensaje de error.  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows.  
  
 **User name**  
 Escriba el nombre de usuario con el que se va a conectar. Esta opción solo está disponible si ha seleccionado la autenticación de Windows para conectarse.  
  
 **Inicio de sesión**  
 Escriba el inicio de sesión con el que va a conectarse. Esta opción solo está disponible si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse.  
  
 **Contraseña**  
 Escriba la contraseña del inicio de sesión. Esta opción solo es editable si ha seleccionado la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectarse.  
  
## <a name="see-also"></a>Ver también  
 [Nodo Administración de directivas &#40;Explorador de objetos&#41;](../../relational-databases/policy-based-management/policy-management-node-object-explorer.md)   
 [Administrar servidores mediante administración basada en directivas](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
