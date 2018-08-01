---
title: Agregar parámetros a un informe para dispositivos móviles | Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 113cb057-deec-40eb-abc8-f35d3900eaa6
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1a854a49884c6a2f1bd93794a7854d30dc1e2d3d
ms.sourcegitcommit: d4392c68eb5f15b175165cf03ef8253565323d68
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/31/2018
ms.locfileid: "39359612"
---
# <a name="add-parameters-to-a-mobile-report--reporting-services"></a>Agregar parámetros a un informe para dispositivos móviles | Reporting Services
Puede crear un informe para dispositivos móviles de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] con parámetros para que quienes los consulten puedan filtrarlos. Un informe con parámetros también puede ser el destino de una [obtención de detalles de un informe de origen](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md). 

Para crear un informe para dispositivos móviles con parámetros, hay que empezar con un conjunto de datos compartido que tenga al menos un parámetro. Obtenga información sobre cómo [crear parámetros en un conjunto de datos compartido](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md). Los informes para dispositivos móviles no admiten valores null para los parámetros predeterminados, con lo cual que asegúrese de que los parámetros tienen valores predeterminados que no sean null.

Después de agregar parámetros a un informe móvil, se crea una dirección URL para [abrir el informe con los parámetros de cadena de consulta](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md). 

1. En la barra superior del portal web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] , seleccione **Nuevo** > **Informe móvil**.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. Seleccione la pestaña **Datos** situada en la esquina superior izquierda del [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)].   
  
3. En la esquina superior derecha, seleccione **Agregar datos**.  
  
4. Seleccione **Servidor de informes**y, seguidamente, seleccione un servidor.  
  
5. Vaya a los conjuntos de datos compartidos de ese servidor y seleccione uno que tenga parámetros.  
  
   En la cuadrícula, verá los datos del conjunto de datos. El círculo verde con corchetes **{ }** marca un conjunto de datos con un parámetro.  
     
   ![SSMRP_PforParam](../../reporting-services/mobile-reports/media/ssmrp-pforparam.png)  
  
6. Seleccione el engranaje de la pestaña y, luego, seleccione **Param {}**.  
  
   ![SSMRP_ParamWheel](../../reporting-services/mobile-reports/media/ssmrp-paramwheel.png)  
  
7. Seleccione el elemento de informe que va a pasar los valores al parámetro.  
  
   ![SSMRP_SetParam](../../reporting-services/mobile-reports/media/ssmrp-setparam.png)  
     
8. Seleccione **Vista previa** para ver cómo quedará el informe. En este informe, la lista de selección usa el parámetro Category.

   ![sql-server-mobile-report-publisher-Selection-List-View-No-Selection](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-view-no-selection.png) 
   
9. Cuando selecciona un valor en la lista de selección, el informe se filtra según ese valor; en este caso, Accesorios.

   ![sql-server-mobile-report-publisher-Selection-List-Category-Selected](../../reporting-services/mobile-reports/media/sql-server-mobile-report-publisher-selection-list-category-selected.png)   
  
### <a name="see-also"></a>Vea también  
-  [Abrir un informe móvil con parámetros específicos de cadena de consulta](../../reporting-services/mobile-reports/open-a-mobile-report-with-specific-query-string-parameters-reporting-services.md)
-  [Agregar obtención de detalles de un informe para dispositivos móviles a otros informes para dispositivos móviles o direcciones URL](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)
-  [Crear un conjunto de datos compartido o un conjunto de datos incrustado](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  

