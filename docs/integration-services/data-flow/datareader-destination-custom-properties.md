---
title: Propiedades personalizadas del destino DataReader | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 38c0854947ee9b853d8638593aea1e60d40941ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726937"
---
# <a name="datareader-destination-custom-properties"></a>Propiedades personalizadas del destino DataReader

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El destino DataReader tiene propiedades personalizadas y propiedades comunes a todos los componentes de flujo de datos.  
  
 En la tabla siguiente se describen las propiedades personalizadas del destino DataReader. Todas las propiedades excepto **DataReader** son de lectura y escritura.  
  
|Nombre de propiedad|Tipo de datos|Descripción|  
|-------------------|---------------|-----------------|  
|DataReader|String|Nombre de clase del destino DataReader.|  
|FailOnTimeout|Boolean|Indica si generar un error cuando se produce un **ReadTimeout** . El valor predeterminado de esta propiedad es **False**.|  
|ReadTimeout|Integer|Número de milisegundos que transcurren antes de que se agote el tiempo de espera. El valor predeterminado de esta propiedad es 30000 (30 segundos).|  
  
 La entrada y las columnas de entrada del destino DataReader no tienen ninguna propiedad personalizada.  
  
 Para más información, consulte [DataReader Destination](../../integration-services/data-flow/datareader-destination.md).  
  
## <a name="see-also"></a>Consulte también  
 [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
