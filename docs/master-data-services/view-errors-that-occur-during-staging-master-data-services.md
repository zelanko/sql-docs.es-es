---
title: Ver los errores que se producen durante el almacenamiento provisional (Master Data Services)|Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
caps.latest.revision: 8
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: de3c6c2f487dd10b6d55a25c802339a14a67a055
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="view-errors-that-occur-during-staging-master-data-services"></a>Ver los errores que se producen durante el almacenamiento provisional (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede ver los errores que se producen durante el proceso de almacenamiento provisional. En la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , hay dos vistas que muestran errores:  
  
-   stg.viw_name_MemberErrorDetails para las actualizaciones de miembros hoja o consolidados.  
  
-   stg.viw_name_RelationshipErrorDetails para las actualizaciones de la relación de la jerarquía.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   En la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , debe tener permisos SELECT en las vistas stg.viw_name_MemberErrorDetails o stg.viw_name_RelationshipErrorDetails.  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-view-staging-errors"></a>Para ver errores de almacenamiento provisional  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Abra una nueva consulta.  
  
3.  Escriba el texto siguiente, reemplazando el nombre con el nombre de su tabla de ensayo; por ejemplo, viw_Product_MemberErrorDetails.  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  Ejecute la consulta. Los detalles del error se muestran en el campo **ErrorDescription** .  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para obtener más información sobre mensajes de error, consulte [Errores del proceso de almacenamiento provisional &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Solucionar problemas del proceso de almacenamiento provisional (Master Data Services)](http://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  

