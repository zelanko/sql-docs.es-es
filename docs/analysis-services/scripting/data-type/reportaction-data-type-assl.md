---
title: Tipo de datos ReportAction (ASSL) | Documentos de Microsoft
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e99b4259600f9bd6c288826e452f1d763316b2e1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="reportaction-data-type-assl"></a>Tipo de datos ReportAction (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Define un tipo de datos derivado que representa una acción que genera una [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<ReportAction>  
   <!-- The following elements extend Action -->  
   <ReportServer>...</ReportServer>  
   <Path>...</Path>  
   <ReportParameters>...</ReportParameters>  
   <ReportFormatParameters>...</ReportFormatParameters>  
</ReportAction>  
```  
  
## <a name="data-type-characteristics"></a>Características del tipo de datos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipos de datos base|[Acción](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|Tipos de datos derivados|Ninguno|  
  
## <a name="data-type-relationships"></a>Relaciones entre tipos de datos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|Ninguno|  
|Elementos secundarios|[Ruta de acceso](../../../analysis-services/scripting/properties/path-element-assl.md), [ReportFormatParameters](../../../analysis-services/scripting/collections/reportformatparameters-element-assl.md), [ReportParameters](../../../analysis-services/scripting/collections/reportparameters-element-assl.md), [ReportServer](../../../analysis-services/scripting/properties/reportserver-element-assl.md)|  
|Elementos derivados|[Acción](../../../analysis-services/scripting/objects/action-element-assl.md) ([acciones](../../../analysis-services/scripting/collections/actions-element-assl.md) colección de [cubo](../../../analysis-services/scripting/objects/cube-element-assl.md) o [perspectiva](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Comentarios  
 El servidor de informes responde a las solicitudes basadas en URL para los informes. La acción de informe se define con un tipo *Report*. Los recursos y parámetros se envían al servidor cuando se crea la acción. El servidor expone la acción como una acción de conjunto de filas de tipos.  
  
 El elemento correspondiente en el modelo de objetos de Analysis Management Objects (AMO) es <xref:Microsoft.AnalysisServices.ReportAction>.  
  
## <a name="see-also"></a>Vea también  
 [Analysis Services Scripting Language tipos de datos XML & #40; ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
