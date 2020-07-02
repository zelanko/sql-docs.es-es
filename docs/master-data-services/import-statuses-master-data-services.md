---
title: Estados de importación
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 306577c5-e7d7-4cff-aff4-efb5c6354036
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 40cc57e3d8ba66c36c52906f5d134325178a37e4
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812961"
---
# <a name="import-statuses-master-data-services"></a>Estados de importación (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  En el área funcional **Administración de integraciones**, en la página **Lotes de almacenamiento provisional**, son posibles los estados siguientes.  
  
|Estado|Descripción|Status_ID|  
|------------|-----------------|----------------|  
|En cola para ejecutar|No se ha iniciado el procesamiento del lote.|1|  
|En ejecución|Se está procesando el lote.|2|  
|Completado|Se ha terminado de procesar el lote.|3|  
|En cola para borrar|El lote ha finalizado su procesamiento y se borrará.|4|  
|Desactivado|Se ha borrado el lote.|5|  
  
## <a name="see-also"></a>Consulte también  
 [Información general: importación de datos de tablas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)  
  
  
