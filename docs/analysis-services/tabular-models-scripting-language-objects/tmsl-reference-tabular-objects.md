---
title: Definiciones de objetos tabulares modelo Scripting Language (TMSL) | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 458f39a28295abe431be00ca59fc49d56dd29cb7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="tmsl-reference---tabular-objects"></a>Referencia TMSL: objetos tabulares
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Las aplicaciones que crean, consumir o administrar bases de datos tabulares o que se conectan a una instancia de SQL Server 2016 Analysis Services en modo tabular, puede usar el Tabular Model Scripting Language (TMSL) para los comandos y las representaciones de objeto en formato JSON.  
  
 Este artículo documentan los objetos principales del esquema TMSL utilizado en los scripts generados por SQL Server Management Studio, SQL Server Data Tools (SSDT) y PowerShell de AMO.  
  
 Las definiciones de objeto en JSON y utilizan en los comandos TMSL como Create, Alter y eliminar. Vea [comandos de Tabular Model Scripting Language &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) para obtener una lista de comandos.  
  
## <a name="main-objects"></a>Objetos principales  
 En la tabla siguiente es la lista de los objetos más usados en el script de TMSL.  
  
|||  
|-|-|  
|[Objeto de base de datos &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|Define una base de datos Tabular en el nivel de compatibilidad 1200 o superior, en función de un modelo del mismo nivel.|  
|[Objeto de modelo &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|Define un modelo Tabular en el nivel de compatibilidad 1200 o superior.|  
|[Objeto de orígenes de datos &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|Define una conexión a un origen de datos que se utilizan durante la importación para cargar el modelo, o para el acceso a través de consultas cuando el modelo está en modo DirectQuery.|  
|[Tables, objeto &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|Especifica las tablas del modelo.|  
|[Objeto de particiones &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|Define el almacenamiento de conjuntos de filas de tabla, incluidas las tablas calculadas.|  
|[Objeto de relaciones &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|Define las relaciones entre tablas.|  
|[Objeto de los roles &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|Define permisos, pertenencia y los filtros de seguridad que controlan el acceso a datos y las operaciones.|  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  
