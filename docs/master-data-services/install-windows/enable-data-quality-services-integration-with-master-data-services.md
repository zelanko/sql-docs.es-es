---
title: Habilitar la integración de Data Quality Services con Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: ab32938d-a80e-4106-80d4-94b2de3d67dc
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 20a85b00207d010baa7d82f03e756deed32c73c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65480205"
---
# <a name="enable-data-quality-services-integration-with-master-data-services"></a>Habilitar la integración de Data Quality Services con Master Data Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

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
  
  
