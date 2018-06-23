---
title: Elemento Schema (ASSL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Schema Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Schema
helpviewer_keywords:
- Schema element
ms.assetid: 4b6375fb-7ad8-4d5f-88b1-abd3da2654db
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 130d1363a007fb51db3bc7b39efcae4d9140c368
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114139"
---
# <a name="schema-element-assl"></a>Elemento Schema (ASSL)
  Contiene el esquema de la vista del origen de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataSourceView>  
   ...  
   <Schema>...</Schema>  
   ...  
</DataSourceView>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|esquema|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DataSourceView](../objects/datasourceview-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El `Schema` se representa usando el  formato del lenguaje de definición de esquemas XML (XSD) de conjuntos de datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework, con algunas extensiones para los conjuntos de datos y otras específicas para este uso dentro del lenguaje de definición de datos (DDL). Los conjuntos de datos definen una asignación flexible de XSD a un esquema relacional pero a continuación, devuelven XSD en un más la forma canónica. Solo esta forma canónica es válida dentro de los orígenes de datos.  
  
 El elemento que corresponde al elemento primario de `Schema` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  