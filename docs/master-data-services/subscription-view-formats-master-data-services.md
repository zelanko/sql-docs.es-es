---
description: Formatos de vista de suscripciones (Master Data Services)
title: Formatos de vista de suscripciones
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: ff1e2566-ac8f-467d-a6d9-12c3f13879b9
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ac58c9c1edfce6b02f48c31e220d37d842b18527
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456756"
---
# <a name="subscription-view-formats-master-data-services"></a>Formatos de vista de suscripciones (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Según la entidad o la jerarquía derivada que seleccione, están disponibles los formatos siguientes para la vista de suscripciones.  
  
## <a name="subscription-view-formats"></a>Formatos de vista de suscripciones  
  
|Nombre|Descripción|  
|----------|-----------------|  
|**Miembros hoja**|Contiene miembros hoja y sus valores de atributo asociados.|  
|**Historial de miembros hoja**|Contiene los datos históricos de los miembros hoja y los valores de atributo asociados. El formato de vista es el estilo Dimensión de variación lenta tipo 4.|  
|**DVL de miembros hoja tipo 2**|Contiene los datos históricos y actuales de los miembros hoja y los valores de atributo asociados. El formato de vista es el estilo Dimensión de variación lenta tipo 2.|  
|**Miembros consolidados**|Contiene miembros consolidados y sus valores de atributo asociados.|  
|**Historial de miembros consolidados**|Contiene los datos históricos de los miembros consolidados y los valores de atributo asociados. El formato de vista es el estilo Dimensión de variación lenta tipo 4.|  
|**DVL de miembros consolidados tipo 2**|Contiene los datos históricos y actuales de los miembros consolidados y los valores de atributo asociados. El formato de vista es el estilo Dimensión de variación lenta tipo 2.|  
|**Miembros de la colección**|Contiene una lista de colecciones y sus valores de atributo asociados.|  
|**Colecciones**|Contiene una lista de colecciones y los miembros de cada una, junto con valores de ponderación y criterio de ordenación.|  
|**Historial de miembros de colección**|Contiene los datos históricos de los miembros de colección y los valores de atributo asociados. El formato de vista es el estilo Dimensión de variación lenta tipo 4.|  
|**DVL de miembros de colección tipo 2**|Contiene los datos históricos y actuales de los miembros de colección y los valores de atributo asociados. El formato de vista es el estilo Dimensión de variación lenta tipo 2.|  
|**Elemento primario/secundario explícito**|Contiene las estructuras de jerarquía explícitas para una entidad en formato de elemento secundario y primario.|  
|**Niveles explícitos**|Contiene las estructuras de jerarquía explícitas para una entidad en formato de nivel.|  
|**Elemento secundario/primario derivado (Vista de jerarquía derivada)**|Contiene una estructura de jerarquía derivada en formato elemento secundario y primario.|  
|**Niveles derivados (Vista de jerarquía derivada)**|Contiene una estructura de jerarquía derivada en formato de nivel.|  
  
## <a name="see-also"></a>Consulte también  
 [Información general: exportar datos &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)   
 [Crear una vista de suscripciones para exportar datos &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
  
