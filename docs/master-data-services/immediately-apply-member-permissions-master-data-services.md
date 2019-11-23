---
title: Aplicar inmediatamente los permisos de los miembros
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], applying permissions immediately
- permissions [Master Data Services], applying member permissions immediately
ms.assetid: 5b16de66-5c39-49f5-992f-402a9eb319aa
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 82ad2fad9645d3d8277abac6328d23c7b18a0c94
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729219"
---
# <a name="immediately-apply-member-permissions-master-data-services"></a>Aplicar inmediatamente los permisos de los miembros (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], en lugar de esperar a que la seguridad de los miembros se aplique a intervalos normales, puede aplicar los permisos de miembro inmediatamente.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe tener permiso para ejecutar el procedimiento almacenado mds.udpSecurityMemberProcessRebuildModel en la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para obtener más información, consulte [Seguridad de objetos de base de datos &#40;Master Data Services&#41;](../master-data-services/database-object-security-master-data-services.md).  
  
### <a name="to-immediately-apply-hierarchy-member-permissions"></a>Para aplicar inmediatamente permisos de miembro de jerarquía  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Cree una nueva consulta.  
  
3.  Escriba el siguiente texto y reemplace *database* con el nombre de su base de datos y *Model_Name* con el nombre del modelo.  
  
    ```  
    USE [database];  
    GO  
  
    DECLARE @Model_ID INT;  
    SELECT @Model_ID = ID FROM mdm.tblModel WHERE [Name] = N'Model_Name';  
    EXEC [mdm].[udpSecurityMemberProcessRebuildModel] @Model_ID=@Model_ID, @ProcessNow=1;  
    GO  
    ```  
  
4.  Ejecuta la consulta.  
  
## <a name="see-also"></a>Vea también  
 [Asignar los permisos de los miembros de una jerarquía &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Permisos de miembros de la jerarquía &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
