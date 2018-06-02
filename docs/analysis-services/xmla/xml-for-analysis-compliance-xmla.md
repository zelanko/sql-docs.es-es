---
title: XML for Analysis (XMLA) cumplimiento | Documentos de Microsoft
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b618fdd8cca3faed72afb0276f18cd928a3f31f7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576887"
---
# <a name="xml-for-analysis-xmla-compliance"></a>XML for Analysis (XMLA) cumplimiento
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]  

  La especificación XML for Analysis 1.1 describe un estándar abierto que admite el acceso a datos a orígenes de datos que residen en World Wide Web. Este tema detalla el nivel de compatibilidad con la especificación de XML for Analysis 1.1 que sea compatible con Azure Analysis Services y SQL Server Analysis Services.  
  
## <a name="compliant-items"></a>Elementos compatibles  
Analysis Services es compatible con todos los elementos obligatorios enumerados en la especificación de XML for Analysis 1.1. Además, Analysis Services no implementa el elemento opcional siguiente descrito en la especificación de XML for Analysis 1.1.  
  
|Elemento|Especificación|Implementación|  
|----------|-------------------|--------------------|  
|Compatibilidad de sesión|Los elementos de encabezado SOAP que se enumeran en la sección"Disponibilidad de estados en XML for Analysis" de la especificación de XML for Analysis 1.1.|Todos los elementos de encabezado SOAP enumerados son compatibles con Analysis Services, tal como se describe en la especificación.|  
  
## <a name="extensions"></a>Extensiones  
 Analysis Services también extiende la especificación XML for Analysis 1.1 para admitir las siguientes características adicionales y capacidades.  
  
|Elemento|Especificación|Implementación|  
|----------|-------------------|--------------------|  
|Negociación del protocolo|La especificación de XML for Analysys 1.1 no contiene ninguna información|Elemento de encabezado de ProtocolCapabilities agregado por Analysis Services para admitir negociación de capacidades de protocolo.|  
|Comandos XML for Analysis (XMLA) compatibles con el método Discover|La especificación de XML for Analysis 1.1 admite los siguientes comandos:<br /><br /> [Elemento Statement &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Analysis Services admite los siguientes comandos:<br /><br /> [Elemento ALTER &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [Elemento de la copia de seguridad &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [Elemento de lote &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [Elemento BeginTransaction &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [Elemento Cancel &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [Elemento ClearCache &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [Elemento CommitTransaction &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [Crear el elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [Eliminar elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [Elemento DesignAggregations &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [Elemento DROP &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [Insertar elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [Bloquear elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [Elemento MergePartitions &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [Elemento NotifyTableChange &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [Procesar el elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Elemento restore &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [Elemento RollbackTransaction &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [Elemento Statement &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [Elemento Subscribe &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [Elemento Synchronize &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [Elemento Unlock &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [Actualizar elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [Elemento UpdateCells &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|Errores de la columna en conjuntos de filas tabulares|No se enumera en la especificación de XML for Analysis 1.1.|El [Error](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) elemento es usado por Analysis Services para informar de errores para los elementos de columna incluidos en un [fila](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) elemento.|  
  
## <a name="see-also"></a>Vea también
 [Referencia XML for Analysis &#40;XMLA&#41;](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
