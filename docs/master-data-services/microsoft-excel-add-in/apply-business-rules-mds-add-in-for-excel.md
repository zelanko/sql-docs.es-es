---
title: "Aplicar reglas de negocios (complemento MDS para Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: cd106345-f561-4966-88d3-a69139b2bd78
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# Aplicar reglas de negocios (complemento MDS para Excel)
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] , puede aplicar reglas de negocios cuando desee validar datos y confirmar que son válidos. Puede corregir validaciones y volver a publicar los datos.  
  
> [!NOTE]  
>  La validación de datos aparece automáticamente al publicar datos. Para obtener más información, consulte [Validación &#40;Master Data Services&#41;](../../master-data-services/validation-master-data-services.md).  
  
## Requisitos previos  
 Para realizar este procedimiento:  
  
-   Debe tener acceso al área funcional **Explorador** .  
  
-   Debe tener una hoja de cálculo activa que contenga datos administrados por MDS.  
  
### Para aplicar reglas de negocios  
  
1.  En el grupo **Publicar y validar** , haga clic **Aplicar las reglas**.  
  
    > [!NOTE]  
    >  El número de miembros (filas) que se validan al mismo tiempo depende de un valor de [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]. Para más información, consulte [Business Rule Settings](../../master-data-services/system-settings-master-data-services.md#BusinessRules).  
  
2.  Los datos se validan comparándolos con las reglas de negocios y se muestran dos columnas de estado. Si estas columnas no se muestran automáticamente, en el grupo **Publicar y validar** , haga clic en **Mostrar estado** para verlas.  
  
## Vea también  
 [Información general: Importación de datos desde Excel &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  