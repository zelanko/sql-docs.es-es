---
title: Definiciones de objetos en forma de tabla del modelo Scripting Language (TMSL) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: de968c32f8c00132157a5b1b7a6682adc7148446
ms.sourcegitcommit: b75fc8cfb9a8657f883df43a1f9ba1b70f1ac9fb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851750"
---
# <a name="tmsl-reference---tabular-objects"></a>Referencia de TMSL: objetos tabulares
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Las aplicaciones que crear, usar o administrar bases de datos tabulares o que se conectan a una instancia de SQL Server 2016 Analysis Services en modo tabular, puede usar el Tabular Model Scripting Language (TMSL) para los comandos y las representaciones de objeto en formato JSON.  
  
 Este artículo documenta los objetos del esquema TMSL usado en los scripts generados por SQL Server Management Studio, SQL Server Data Tools (SSDT) y PowerShell AMO principales.  
  
 Las definiciones de objeto en JSON y utilizan en los comandos TMSL, como Create, Alter y eliminación. Consulte [comandos de Tabular Model Scripting Language &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) para obtener una lista de comandos.  
  
## <a name="main-objects"></a>Objetos principales  
 En la tabla siguiente es la lista de los objetos usados con más frecuencia en el script TMSL.  
  
|||  
|-|-|  
|[Objeto de base de datos &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|Define una base de datos Tabular en el nivel de compatibilidad 1200 o superior, basado en un modelo del mismo nivel.|  
|[Objeto de modelo &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|Define un modelo Tabular en el nivel de compatibilidad 1200 o superior.|  
|[Objeto DataSources &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|Define una conexión a un origen de datos que se utilizan durante la importación para cargar el modelo, o de paso a través de las consultas cuando el modelo está en el modo DirectQuery.|  
|[Tables, objeto &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|Especifica las tablas del modelo.|  
|[Objeto Partitions &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|Define el almacenamiento de conjuntos de filas de tabla, incluidas las tablas calculadas.|  
|[Objeto Relationships &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|Define las relaciones entre tablas.|  
|[Objeto roles &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|Define los permisos, la pertenencia y los filtros de seguridad que controlan el acceso a datos y las operaciones.|  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
