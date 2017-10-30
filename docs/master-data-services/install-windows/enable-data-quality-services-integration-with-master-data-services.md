---
title: "Habilitar la integración de Data Quality Services con Master Data Services | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
caps.latest.revision: 5
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 50488f539ba00055f4b515a41dca47594c5d3f0d
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>Habilitar la integración de Data Quality Services con Master Data Services
  En el [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], Data Quality Services (DQS) proporciona la funcionalidad de coincidencia. Esta funcionalidad debe habilitarse para poder usarse.  
  
## <a name="prerequisites"></a>Requisitos previos  
  
-   Una aplicación web y una base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] deben existir.  
  
-   La característica Data Quality Services y Data Quality Client deben estar instalados en la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos MDS. Para más información, consulte [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
### <a name="to-enable-data-quality-services-integration"></a>Para habilitar la integración con Data Quality Services  
  
1.  Abra [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
2.  En el panel izquierdo, haga clic en **Configuración web**.  
  
3.  En la página **Configuración web** , seleccione el sitio web y la aplicación web.  
  
4.  En la sección **Habilitar la integración DQS** , haga clic en **Habilitar la integración con Data Quality Services**.  
  
5.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Coincidencia de calidad de datos en el Complemento MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)   
 [Complemento Master Data Services para Microsoft Excel](../../master-data-services/microsoft-excel-add-in/master-data-services-add-in-for-microsoft-excel.md)   
 [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  

