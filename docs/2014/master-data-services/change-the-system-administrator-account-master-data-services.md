---
title: Cambiar la cuenta de administrador del sistema (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], changing
ms.assetid: cf30312e-4338-49a7-90f0-6e4f7b431ff8
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 4a10b20332059c9cf1b9aed41caf462faf96414e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925876"
---
# <a name="change-the-system-administrator-account-master-data-services"></a>Cambiar la cuenta de administrador del sistema (Master Data Services)
  Puede cambiar la cuenta de usuario que se designa como la [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] administrador del sistema.  
  
> [!WARNING]  
>  Al completar este procedimiento, se elimina la cuenta de usuario del administrador del sistema anterior.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe agregar el nombre de usuario del nuevo administrador a la lista de usuarios de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Para obtener más información, consulte [agregar un usuario &#40;Master Data Services&#41;](add-a-user-master-data-services.md).  
  
-   Debe tener permiso para ver mdm.tblUser y ejecutar el procedimiento almacenado mdm.udpSecurityMemberProcessRebuildModel en la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obtener más información, consulte [Seguridad de objetos de base de datos &#40;Master Data Services&#41;](../../2014/master-data-services/database-object-security-master-data-services.md).  
  
### <a name="to-change-the-administrator-account"></a>Para cambiar la cuenta del administrador  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  En Tmd.tbluser, busque el usuario que será el nuevo administrador y copie el valor de la `SID` columna.  
  
3.  Cree una nueva consulta.  
  
4.  Escriba el texto siguiente, reemplazando *DOMINIO\nombre_de_usuario* con el nombre de usuario del nuevo administrador y *SID* con el valor que copió en el paso 2.  
  
    ```  
    EXEC [mdm].[udpSecuritySetAdministrator] @UserName='DOMAIN\user_name', @SID = 'SID', @PromoteNonAdmin = 1  
    ```  
  
5.  Ejecuta la consulta.  
  
## <a name="see-also"></a>Vea también  
 [Administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)  
  
  
