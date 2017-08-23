---
title: Combinar conflictos (Master Data Services) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 797219ad-5109-4666-94d3-dd1d59440a33
caps.latest.revision: 5
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cd232ee139207f8ee78b0a5c549c81a26ee1e5e1
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="merge-conflicts-master-data-services"></a>Conflictos de combinación (Master Data Services)
  En [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], si intenta publicar los datos que ha cambiado otro usuario, se producirá un error de combinación en la publicación. Para resolver este error, puede ejecutar los conflictos de fusión mediante combinación y volver a publicar los cambios.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   Como mínimo, debe tener el permiso Actualizar para el objeto de modelo hoja en la entidad que vaya a actualizar.  
  
### <a name="to-merge-conflicts"></a>Para conflictos de combinación  
  
1.  En la página **Explorador** , actualice el atributo de miembro.  
  
2.  Si otro usuario ha cambiado el mismo atributo de miembro, se abre el cuadro de diálogo **Conflictos de combinación** .  
  
3.  En el cuadro de diálogo **Merge Conflicts** (Conflictos de combinación), puede:  
  
    -   Elegir **Más reciente** y hacer clic en **Aplicar** para deshacer los cambios pendientes y volver a cargar la versión más reciente desde el servidor.  
  
    -   Elegir **Original** y hacer clic en **Aplicar** para aplicar la versión original en la hoja de cálculo.  
  
    -   Elegir **Suyo** y hacer clic en **Aplicar** para conservar los cambios locales existentes.  
  
4.  Tras hacer clic en **Aplicar**, puede realizar cambios adicionales y volver a publicarlos. O puede hacer clic en **Cancelar** para cancelar la actualización y volver a cargar la última versión desde el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Miembros &#40;Master Data Services&#41;](../master-data-services/members-master-data-services.md)  
  
  
