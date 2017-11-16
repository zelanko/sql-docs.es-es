---
title: Definiciones de objetos tabulares modelo Scripting Language (TMSL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 486f0507-cec6-4672-b947-0bb61d1cbc46
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3f69f6b59054b7fb1880757271b290874448373d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="tmsl-reference---tabular-objects"></a>Referencia TMSL: objetos tabulares

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

  Las aplicaciones que crean, consumir o administrar bases de datos tabulares o que se conectan a una instancia de SQL Server 2016 Analysis Services en modo tabular, puede usar el Tabular Model Scripting Language (TMSL) para los comandos y las representaciones de objeto en formato JSON.  
  
 Este artículo documentan los objetos principales del esquema TMSL utilizado en los scripts generados por SQL Server Management Studio, SQL Server Data Tools (SSDT) y PowerShell de AMO.  
  
 Las definiciones de objeto en JSON y utilizan en los comandos TMSL como Create, Alter y eliminar. Vea [comandos de Tabular modelo de lenguaje de Scripting &#40; TMSL &#41; ](../../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md) para obtener una lista de comandos.  
  
## <a name="main-objects"></a>Objetos principales  
 En la tabla siguiente es la lista de los objetos más usados en el script de TMSL.  
  
|||  
|-|-|  
|[Objeto de base de datos &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/database-object-tmsl.md)|Define una base de datos Tabular en el nivel de compatibilidad 1200 o superior, en función de un modelo del mismo nivel.|  
|[Objeto de modelo &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/model-object-tmsl.md)|Define un modelo Tabular en el nivel de compatibilidad 1200 o superior.|  
|[Objeto de orígenes de datos &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/datasources-object-tmsl.md)|Define una conexión a un origen de datos que se utilizan durante la importación para cargar el modelo, o para el acceso a través de consultas cuando el modelo está en modo DirectQuery.|  
|[Objeto de tablas &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/tables-object-tmsl.md)|Especifica las tablas del modelo.|  
|[Objeto de particiones &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/partitions-object-tmsl.md)|Define el almacenamiento de conjuntos de filas de tabla, incluidas las tablas calculadas.|  
|[Objeto de relaciones &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/relationships-object-tmsl.md)|Define las relaciones entre tablas.|  
|[Objeto de roles &#40; TMSL &#41;](../../analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl.md)|Define permisos, pertenencia y los filtros de seguridad que controlan el acceso a datos y las operaciones.|  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)  
  
  

