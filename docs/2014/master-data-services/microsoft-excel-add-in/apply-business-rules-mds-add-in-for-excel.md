---
title: Aplicar reglas de negocios (complemento MDS para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2722e678de98bbfbf5a1181a69101fbe2a9427d8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62923959"
---
# <a name="apply-business-rules-mds-add-in-for-excel"></a>Aplicar reglas de negocios (complemento MDS para Excel)
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] , puede aplicar reglas de negocios cuando desee validar datos y confirmar que son válidos. Puede corregir validaciones y volver a publicar los datos.  
  
> [!NOTE]  
>  La validación de datos aparece automáticamente al publicar datos. Para obtener más información, consulte [Procedimiento almacenado de validación &#40;Master Data Services&#41;](../validation-stored-procedure-master-data-services.md).  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe tener acceso al área funcional **Explorador** .  
  
-   Debe tener una hoja de cálculo activa que contenga datos administrados por MDS.  
  
### <a name="to-apply-business-rules"></a>Para aplicar reglas de negocios  
  
1.  En el grupo **Publicar y validar** , haga clic **Aplicar las reglas**.  
  
    > [!NOTE]  
    >  El número de miembros (filas) que se validan al mismo tiempo depende de un valor de [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. Para más información, consulte [Business Rule Settings](../system-settings-master-data-services.md#BusinessRules).  
  
2.  Los datos se validan comparándolos con las reglas de negocios y se muestran dos columnas de estado. Si estas columnas no se muestran automáticamente, en el grupo **Publicar y validar** , haga clic en **Mostrar estado** para verlas.  
  
## <a name="see-also"></a>Vea también  
 [Publicar datos &#40;complemento MDS para Excel&#41;](overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
