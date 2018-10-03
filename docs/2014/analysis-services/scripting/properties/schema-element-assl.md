---
title: Elemento Schema (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5b8f9ab11698c2e0e73436abb3506ca38c45afe6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218809"
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|esquema|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[Elemento DataSourceView](../objects/datasourceview-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 El `Schema` se representa usando el  formato del lenguaje de definición de esquemas XML (XSD) de conjuntos de datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework, con algunas extensiones para los conjuntos de datos y otras específicas para este uso dentro del lenguaje de definición de datos (DDL). Los conjuntos de datos definen una asignación flexible de XSD a un esquema relacional pero a continuación, devuelven XSD en un más la forma canónica. Solo esta forma canónica es válida dentro de los orígenes de datos.  
  
 El elemento que se corresponde con el elemento primario de `Schema` en el objeto de Analysis Management Objects (AMO) es el modelo <xref:Microsoft.AnalysisServices.DataSourceView>.  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
