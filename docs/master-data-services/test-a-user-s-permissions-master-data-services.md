---
title: Prueba un usuario &#39; s permisos (Master Data Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83a03b85-ea7f-4b4a-b19b-f7eca534ffae
caps.latest.revision: 4
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 125c5cffc68dd80688242636c455fb26e4129263
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="test-a-user39s-permissions-master-data-services"></a>Prueba un usuario &#39; s permisos (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede crear un usuario y un registro de pruebas en la aplicación web para probar los permisos. Cuando un usuario intenta tener acceso a la dirección URL de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , se autentican las credenciales del usuario. En Internet Explorer, la configuración de seguridad controla si esto ocurre automáticamente o si el usuario debe escribir un nombre de usuario y una contraseña. Para cambiar estos valores, complete los siguientes pasos:  
  
### <a name="to-test-a-users-security"></a>Para probar la seguridad de un usuario  
  
1.  En Internet Explorer 7 y versiones posteriores, haga clic en **Herramientas**, **Opciones de Internet**y, a continuación, haga clic en la pestaña **Seguridad** .  
  
2.  Haga clic en **Intranet local** y, a continuación, en el botón **Nivel personalizado** .  
  
3.  En la sección **Autenticación de usuario** , elija **Preguntar por el nombre de usuario y la contraseña**.  
  
4.  La próxima vez que abra la ventana explorador, se le solicitará un nombre de usuario y una contraseña.  
  
## <a name="see-also"></a>Vea también  
 [Seguridad &#40;Master Data Services&#41;](../master-data-services/security-master-data-services.md)  
  
  
