---
title: "Conflictos de combinación (complemento MDS para Excel) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: microsoft-excel-add-in
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cf95978f-a2c5-4325-8606-dbd4e88741b8
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db3056898ea1d48d17fccd5518c184d1469d1640
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
---
# <a name="merge-conflicts-mds-add-in-for-excel"></a>Conflictos de combinación (complemento MDS para Excel)
  En el complemento [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] para Excel, si otro usuario ha cambiado en el servidor, se producirá un error de conflicto en la publicación. Para resolver este error, puede ejecutar los conflictos de fusión mediante combinación y volver a publicar los cambios.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para realizar este procedimiento:  
  
-   Debe disponer de permiso de acceso al área funcional **Explorador** .  
  
-   Como mínimo, debe tener el permiso Actualizar para el objeto de modelo hoja en la entidad que vaya a actualizar.  
  
-   La hoja de cálculo activa debe tener datos administrados por MDS.  
  
-   La hoja de cálculo activa debe tener un error de conflicto después de intentar publicar los cambios.  
  
### <a name="to-merge-conflicts"></a>Para conflictos de combinación  
  
1.  En la hoja de cálculo, seleccione la fila o celda que tiene el error de conflicto.  
  
2.  En el grupo de menús **Publish and Validate** (Publicar y validar), seleccione **Merge Conflicts** (Conflictos de combinación) para abrir el cuadro de diálogo **Merge Conflicts** (Conflictos de combinación).  
  
3.  En el cuadro de diálogo **Merge Conflicts** (Conflictos de combinación), puede:  
  
    -   Elegir **Más reciente** y hacer clic en **Aplicar** para deshacer los cambios pendientes y volver a cargar la versión más reciente desde el servidor.  
  
    -   Elegir **Original** y hacer clic en **Aplicar** para aplicar la versión original en la hoja de cálculo.  
  
    -   Elegir **Suyo** y hacer clic en **Aplicar** para conservar los cambios locales existentes.  
  
4.  Tras hacer clic en **Aplicar**, puede realizar cambios adicionales y volver a publicarlos. O puede hacer clic en **Cancelar** para cancelar la actualización y volver a cargar la última versión desde el servidor.  
  
## <a name="see-also"></a>Ver también  
 [Información general: Importación de datos desde Excel &#40;complemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
  
