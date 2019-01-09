---
title: Probar los permisos de un usuario (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: ad4ee1957f295bf13d0346590f621ca87dc6387f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823409"
---
# <a name="test-a-user39s-permissions-master-data-services"></a>Probar los permisos de un usuario (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede crear un usuario y un registro de pruebas en la aplicación web para probar los permisos. Cuando un usuario intenta tener acceso a la dirección URL de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , se autentican las credenciales del usuario. En Internet Explorer, la configuración de seguridad controla si esto ocurre automáticamente o si el usuario debe escribir un nombre de usuario y una contraseña. Para cambiar estos valores, complete los siguientes pasos:  
  
### <a name="to-test-a-users-security"></a>Para probar la seguridad de un usuario  
  
1.  En Internet Explorer 7 y versiones posteriores, haga clic en **Herramientas**, **Opciones de Internet**y, a continuación, haga clic en la pestaña **Seguridad** .  
  
2.  Haga clic en **Intranet local** y, a continuación, en el botón **Nivel personalizado** .  
  
3.  En la sección **Autenticación de usuario** , elija **Preguntar por el nombre de usuario y la contraseña**.  
  
4.  La próxima vez que abra la ventana explorador, se le solicitará un nombre de usuario y una contraseña.  
  
## <a name="see-also"></a>Consulte también  
 [Seguridad &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
