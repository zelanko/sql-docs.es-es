---
title: XML para el cumplimiento de Analysis (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b801e87576ae4ecf47f6ed828d35eac06c44a94d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="xml-for-analysis-compliance-xmla"></a>Compatibilidad con XML for Analysis (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  La especificación XML for Analysis 1.1 describe un estándar abierto que admite el acceso a datos a orígenes de datos que residen en World Wide Web. Este tema detalla el nivel de compatibilidad con la especificación XML for Analysis 1.1 que sea compatible con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="compliant-items"></a>Elementos compatibles  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cumple con todos los elementos obligatorios enumerados en la especificación para XML for Analysis 1.1. Además, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa el elemento opcional siguiente descrito en la especificación de XML for Analysis 1.1.  
  
|Elemento|Especificación|Implementación|  
|----------|-------------------|--------------------|  
|Compatibilidad de sesión|Los elementos de encabezado SOAP que se enumeran en la sección"Disponibilidad de estados en XML for Analysis" de la especificación de XML for Analysis 1.1.|Todos los elementos de encabezado SOAP enumerados son compatibles con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], tal como se describe en la especificación.|  
  
## <a name="extensions"></a>Extensiones  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también extiende la especificación XML for Analysis 1.1 para admitir las siguientes características y funciones adicionales.  
  
|Elemento|Especificación|Implementación|  
|----------|-------------------|--------------------|  
|Negociación del protocolo|La especificación de XML for Analysys 1.1 no contiene ninguna información|Elemento de encabezado ProtocolCapabilities agregado por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para admitir negociación de capacidades de protocolo.|  
|Comandos XML for Analysis (XMLA) compatibles con el método Discover|La especificación de XML for Analysis 1.1 admite los siguientes comandos:<br /><br /> [Elemento Statement &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite los siguientes comandos:<br /><br /> [Elemento ALTER &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)<br /><br /> [Elemento de la copia de seguridad &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)<br /><br /> [Elemento de lote &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)<br /><br /> [Elemento BeginTransaction &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)<br /><br /> [Elemento Cancel &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)<br /><br /> [Elemento ClearCache &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)<br /><br /> [Elemento CommitTransaction &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)<br /><br /> [Crear el elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)<br /><br /> [Eliminar elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)<br /><br /> [Elemento DesignAggregations &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)<br /><br /> [Elemento DROP &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)<br /><br /> [Insertar elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)<br /><br /> [Bloquear elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)<br /><br /> [Elemento MergePartitions &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)<br /><br /> [Elemento NotifyTableChange &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)<br /><br /> [Procesar el elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)<br /><br /> [Elemento restore &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)<br /><br /> [Elemento RollbackTransaction &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)<br /><br /> [Elemento Statement &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)<br /><br /> [Elemento Subscribe &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)<br /><br /> [Sincronizar el elemento & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)<br /><br /> [Elemento Unlock &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)<br /><br /> [Actualizar elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)<br /><br /> [Elemento UpdateCells &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|  
|Errores de la columna en conjuntos de filas tabulares|No se enumera en la especificación de XML for Analysis 1.1.|El [Error](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) utiliza el elemento [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para informar de errores para los elementos de columna incluidos en un [fila](../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md) elemento.|  
  
## <a name="see-also"></a>Vea también  
 [XML for Analysis & #40; XMLA & #41; Referencia](../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
