---
title: Estados de importación (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 306577c5-e7d7-4cff-aff4-efb5c6354036
caps.latest.revision: 10
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c3905312358c36688e4c20a5a78d6c5504c745aa
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35404127"
---
# <a name="import-statuses-master-data-services"></a>Estados de importación (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En el área funcional **Administración de integraciones** , en la página **Lotes de almacenamiento provisional** , son posibles los estados siguientes.  
  
|Estado|Descripción|Status_ID|  
|------------|-----------------|----------------|  
|En cola para ejecutar|No se ha iniciado el procesamiento del lote.|1|  
|En ejecución|Se está procesando el lote.|2|  
|Completado|Se ha terminado de procesar el lote.|3|  
|En cola para borrar|El lote ha finalizado su procesamiento y se borrará.|4|  
|Desactivado|Se ha borrado el lote.|5|  
  
## <a name="see-also"></a>Ver también  
 [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
  
