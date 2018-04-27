---
title: Ver los errores que se producen durante el almacenamiento provisional (Master Data Services)|Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
caps.latest.revision: 8
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72c22de68a3a07b3f6a21687a7f6d0eae6906d6d
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="view-errors-that-occur-during-staging-master-data-services"></a>Ver los errores que se producen durante el almacenamiento provisional (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede ver los errores que se producen durante el proceso de almacenamiento provisional. En la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , hay dos vistas que muestran errores:  
  
-   stg.viw_name_MemberErrorDetails para las actualizaciones de miembros hoja o consolidados.  
  
-   stg.viw_name_RelationshipErrorDetails para las actualizaciones de la relación de la jerarquía.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   En la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , debe tener permisos SELECT en las vistas stg.viw_name_MemberErrorDetails o stg.viw_name_RelationshipErrorDetails.  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-view-staging-errors"></a>Para ver errores de almacenamiento provisional  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Abra una nueva consulta.  
  
3.  Escriba el texto siguiente, reemplazando el nombre con el nombre de su tabla de ensayo; por ejemplo, viw_Product_MemberErrorDetails.  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  Ejecute la consulta. Los detalles del error se muestran en el campo **ErrorDescription** .  
  
## <a name="next-steps"></a>Next Steps  
 Para obtener más información sobre mensajes de error, consulte [Errores del proceso de almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).  
  
## <a name="see-also"></a>Ver también  
 [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Solucionar problemas del proceso de almacenamiento provisional (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  
