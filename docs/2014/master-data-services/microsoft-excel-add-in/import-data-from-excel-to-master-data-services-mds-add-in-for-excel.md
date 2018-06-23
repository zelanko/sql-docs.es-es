---
title: Publicar datos de Excel en MDS (agregar de MDS para Excel) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 89fce454-a816-4b33-a26a-d1b9741d269b
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f32226602413b1d2a7851d9f66ed0f8395f82e95
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204634"
---
# <a name="publish-data-from-excel-to-mds-mds-add-in-for-excel"></a>Publicar datos de Excel en MDS (complemento MDS para Excel)
  En [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], puede publicar los datos en el repositorio MDS cuando termine de trabajar en Excel y desee guardar los cambios para que otros usuarios tengan acceso a ellos.  
  
> [!NOTE]  
>  -   Al publicar los cambios, se eliminan los comentarios de las celdas administradas por MDS.  
> -   Una fórmula no se admite en una celda administrada por MDS. Una fórmula en una celda administrada por MDS se trata como un valor de texto.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   La hoja de cálculo activa debe contener datos administrados por MDS y debe haber realizado cambios o adiciones a los datos administrados por MDS.  
  
-   Si agrega miembros, no tiene que especificar un valor de **Código** si los códigos para la entidad se generan automáticamente. Para obtener más información, consulte [Creación automática de código &#40;Master Data Services&#41;](../automatic-code-creation-master-data-services.md).  
  
### <a name="to-publish-data-to-the-mds-repository"></a>Publicar datos en el repositorio MDS  
  
1.  En el grupo **Publicar y validar** , haga clic en **Publicar**.  
  
2.  Opcional. Si aparece el cuadro de diálogo **Publicar y anotar** , elija compartir la misma anotación (comentario) para todas las actualizaciones o anotar cada cambio de forma individual.  
  
3.  Opcional. Active la casilla **No volver a mostrar este cuadro de diálogo** . Puede mostrar siempre el cuadro de diálogo en el futuro si elije **Configuración** y activa la casilla **Mostrar el cuadro de diálogo Publicar y anotar al publicar** .  
  
4.  Haga clic en **Publicar**.  
  
> [!NOTE]  
>  Si agrega nuevos miembros (filas) en la hoja de cálculo y no puede publicarlos correctamente en el repositorio MDS, es posible que no tenga el permiso **Actualizar** para todos los atributos de la hoja de cálculo. En la pestaña **Revisar** , en el grupo **Cambios** , haga clic en **Desproteger hoja** e intente publicarla de nuevo.  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Aplicar reglas de negocios &#40;complemento MDS para Excel&#41;](apply-business-rules-mds-add-in-for-excel.md)  
  
## <a name="see-also"></a>Vea también  
 [Publicar datos &#40;complemento MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)   
 [Validar datos &#40;complemento MDS para Excel&#41;](validating-data-mds-add-in-for-excel.md)  
  
  