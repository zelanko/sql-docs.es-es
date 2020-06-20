---
title: Cambiar la cuenta de administrador del sistema (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], changing
ms.assetid: cf30312e-4338-49a7-90f0-6e4f7b431ff8
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6266664bc4e1d1c782ce75a9de4edebe52d11f0c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972035"
---
# <a name="change-the-system-administrator-account-master-data-services"></a>Cambiar la cuenta de administrador del sistema (Master Data Services)
  Puede cambiar la cuenta de usuario designada como [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] Administrador del sistema.  
  
> [!WARNING]  
>  Al completar este procedimiento, se elimina la cuenta de usuario del administrador del sistema anterior.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe agregar el nombre de usuario del nuevo administrador a la lista de usuarios de [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Para obtener más información, vea [Agregar un usuario &#40;Master Data Services&#41;](add-a-user-master-data-services.md).  
  
-   Debe tener permiso para ver mdm.tblUser y ejecutar el procedimiento almacenado mdm.udpSecurityMemberProcessRebuildModel en la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obtener más información, consulte [Seguridad de objetos de base de datos &#40;Master Data Services&#41;](../../2014/master-data-services/database-object-security-master-data-services.md).  
  
### <a name="to-change-the-administrator-account"></a>Para cambiar la cuenta del administrador  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  En MDM. tblUser, busque el usuario que será el nuevo administrador y copie el valor en la `SID` columna.  
  
3.  Cree una nueva consulta.  
  
4.  Escriba el siguiente texto, reemplazando *dominio \ user_name* por el nombre de usuario y el *SID* del nuevo administrador por el valor que copió en el paso 2.  
  
    ```  
    EXEC [mdm].[udpSecuritySetAdministrator] @UserName='DOMAIN\user_name', @SID = 'SID', @PromoteNonAdmin = 1  
    ```  
  
5.  Ejecuta la consulta.  
  
## <a name="see-also"></a>Consulte también  
 [Administradores &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md)  
  
  
