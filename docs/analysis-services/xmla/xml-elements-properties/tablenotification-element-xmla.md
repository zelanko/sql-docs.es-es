---
title: Elemento TableNotification (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3936105d9097099a824510bdbd809c5083fb6cf2
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38047017"
---
# <a name="tablenotification-element-xmla"></a>Elemento TableNotification (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Representa una notificación de tabla para un comando [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md) .  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<TableNotifications>  
   ...  
   <TableNotification>  
      <DbSchemaName>...</DbSchemaName>  
      <DbTableName>...</DbTableName>  
   </TableNotification>  
   ...  
</TableNotifications>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[TableNotifications](../../../analysis-services/xmla/xml-elements-properties/tablenotifications-element-xmla.md)|  
|Elementos secundarios|[DbSchemaName](../../../analysis-services/xmla/xml-elements-properties/dbschemaname-element-xmla.md), [DbTableName](../../../analysis-services/xmla/xml-elements-properties/dbtablename-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
  
## <a name="see-also"></a>Vea también
 [Propiedades &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
