---
title: Elemento ApplyCompression (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ApplyCompression Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#ApplyCompression
- urn:schemas-microsoft-com:xml-analysis#ApplyCompression
- microsoft.xml.analysis.applycompression
helpviewer_keywords:
- ApplyCompression element
ms.assetid: 93e222e5-9371-4fb5-aae0-f50b964cc264
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 21ed16ba8209bc44576a50b1adc58508baa84e78
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="applycompression-element-xmla"></a>Elemento ApplyCompression (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Determina si el comando primario [Backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md) comprimirá el archivo de copia de seguridad.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Backup>  
   ...  
   <ApplyCompression>...</ApplyCompression>  
   ...  
</Backup>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Booleano|  
|Valor predeterminado|True|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
