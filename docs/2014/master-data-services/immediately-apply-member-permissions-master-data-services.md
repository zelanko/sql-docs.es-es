---
title: Aplicar inmediatamente los permisos de los miembros (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- members [Master Data Services], applying permissions immediately
- permissions [Master Data Services], applying member permissions immediately
ms.assetid: 5b16de66-5c39-49f5-992f-402a9eb319aa
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 2f2d400a4ba29ebf042324877ed8d62c2a2f70ef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482984"
---
# <a name="immediately-apply-member-permissions-master-data-services"></a>Aplicar inmediatamente los permisos de los miembros (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], en lugar de esperar a que la seguridad de los miembros se aplique a intervalos normales, puede aplicar los permisos de miembro inmediatamente.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe tener permiso para ejecutar el procedimiento almacenado mds.udpSecurityMemberProcessRebuildModel en la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para obtener más información, consulte [Seguridad de objetos de base de datos &#40;Master Data Services&#41;](database-object-security-master-data-services.md).  
  
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
 [Asignar los permisos de los miembros de una jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Permisos de miembros de la jerarquía &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
