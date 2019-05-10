---
title: Ver los errores que se producen durante el proceso de almacenamiento provisional (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 75b7fb5a1b98f599a07e47101f93268779ca39b9
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/09/2019
ms.locfileid: "65478562"
---
# <a name="view-errors-that-occur-during-the-staging-process-master-data-services"></a>Ver los errores que se producen durante el proceso de almacenamiento provisional (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], puede ver los errores que se producen durante el proceso de almacenamiento provisional. En la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , hay dos vistas que muestran errores:  
  
-   stg.viw_name_MemberErrorDetails para las actualizaciones de miembros hoja o consolidados.  
  
-   stg.viw_name_RelationshipErrorDetails para las actualizaciones de la relación de la jerarquía.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   En la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , debe tener permisos SELECT en las vistas stg.viw_name_MemberErrorDetails o stg.viw_name_RelationshipErrorDetails.  
  
-   Debe ser administrador de modelo. Para obtener más información, vea [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-view-staging-errors"></a>Para ver errores de almacenamiento provisional  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Abra una nueva consulta.  
  
3.  Escriba el texto siguiente, reemplazando el nombre con el nombre de su tabla de ensayo; por ejemplo, viw_Product_MemberErrorDetails.  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  Ejecute la consulta. Los detalles del error se muestran en el campo **ErrorDescription** .  
  
## <a name="next-steps"></a>Pasos siguientes  
 Para obtener más información sobre mensajes de error, consulte [Errores del proceso de almacenamiento provisional &#40;Master Data Services&#41;](../../2014/master-data-services/staging-process-errors-master-data-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md)   
 [Solucionar problemas del proceso de almacenamiento provisional (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  
