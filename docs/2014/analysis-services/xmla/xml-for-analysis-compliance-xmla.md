---
title: XML para el cumplimiento de Analysis (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- compliance [XML for Analysis]
- XML for Analysis, compliance
- XMLA, extended functionality
- XML for Analysis, extended functionality
- XMLA, compliance
- extending XML for Analysis
ms.assetid: d987d320-5581-4454-ad45-68e3a22175b6
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cc7a8da77b72f25a68764636fbe15bc2d9e4ae04
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37267091"
---
# <a name="xml-for-analysis-compliance-xmla"></a>Compatibilidad con XML for Analysis (XMLA)
  La especificación XML for Analysis 1.1 describe un estándar abierto que admite el acceso a datos a orígenes de datos que residen en World Wide Web. Este tema describe el nivel de compatibilidad con la especificación XML for Analysis 1.1 que sea compatible con [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
## <a name="compliant-items"></a>Elementos compatibles  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cumple con todos los elementos obligatorios enumerados en la especificación para XML for Analysis 1.1. Además, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] implementa el elemento opcional siguiente descrito en la especificación de XML for Analysis 1.1.  
  
|Elemento|Especificación|Implementación|  
|----------|-------------------|--------------------|  
|Compatibilidad de sesión|Los elementos de encabezado SOAP que se enumeran en la sección"Disponibilidad de estados en XML for Analysis" de la especificación de XML for Analysis 1.1.|Todos los elementos de encabezado SOAP enumerados son compatibles con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], tal como se describe en la especificación.|  
  
## <a name="extensions"></a>Extensiones  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] también extiende la especificación XML for Analysis 1.1 para admitir las siguientes características y funciones adicionales.  
  
|Elemento|Especificación|Implementación|  
|----------|-------------------|--------------------|  
|Negociación del protocolo|La especificación de XML for Analysys 1.1 no contiene ninguna información|[ProtocolCapabilities](xml-elements-headers/protocolcapabilities-element-xmla.md) agregado por el elemento de encabezado [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para admitir negociación de capacidades de protocolo.|  
|Comandos XML for Analysis (XMLA) compatibles con el método Discover|La especificación de XML for Analysis 1.1 admite los siguientes comandos:<br /><br /> -   [Elemento Statement &#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite los siguientes comandos:<br /><br /> -   [Elemento ALTER &#40;XMLA&#41;](xml-elements-commands/alter-element-xmla.md)<br />-   [Elemento de copia de seguridad &#40;XMLA&#41;](xml-elements-commands/backup-element-xmla.md)<br />-   [Elemento de lote &#40;XMLA&#41;](xml-elements-commands/batch-element-xmla.md)<br />-   [Elemento BeginTransaction &#40;XMLA&#41;](xml-elements-commands/begintransaction-element-xmla.md)<br />-   [Elemento Cancel &#40;XMLA&#41;](xml-elements-commands/cancel-element-xmla.md)<br />-   [Elemento ClearCache &#40;XMLA&#41;](xml-elements-commands/clearcache-element-xmla.md)<br />-   [Elemento CommitTransaction &#40;XMLA&#41;](xml-elements-commands/committransaction-element-xmla.md)<br />-   [Crear elemento &#40;XMLA&#41;](xml-elements-commands/create-element-xmla.md)<br />-   [Eliminar elemento &#40;XMLA&#41;](xml-elements-commands/delete-element-xmla.md)<br />-   [Elemento DesignAggregations &#40;XMLA&#41;](xml-elements-commands/designaggregations-element-xmla.md)<br />-   [Elemento DROP &#40;XMLA&#41;](xml-elements-commands/drop-element-xmla.md)<br />-   [Insertar elemento &#40;XMLA&#41;](xml-elements-commands/insert-element-xmla.md)<br />-   [Bloquear elemento &#40;XMLA&#41;](xml-elements-commands/lock-element-xmla.md)<br />-   [Elemento MergePartitions &#40;XMLA&#41;](xml-elements-commands/mergepartitions-element-xmla.md)<br />-   [Elemento NotifyTableChange &#40;XMLA&#41;](xml-elements-commands/notifytablechange-element-xmla.md)<br />-   [Procesar el elemento &#40;XMLA&#41;](xml-elements-commands/process-element-xmla.md)<br />-   [Elemento restore &#40;XMLA&#41;](xml-elements-commands/restore-element-xmla.md)<br />-   [Elemento RollbackTransaction &#40;XMLA&#41;](xml-elements-commands/rollbacktransaction-element-xmla.md)<br />-Elemento SetPasswordEncryptionKey<br />-   [Elemento Statement &#40;XMLA&#41;](xml-elements-commands/statement-element-xmla.md)<br />-   [Elemento Subscribe &#40;XMLA&#41;](xml-elements-commands/subscribe-element-xmla.md)<br />-   [Elemento Synchronize &#40;XMLA&#41;](xml-elements-commands/synchronize-element-xmla.md)<br />-   [Elemento Unlock &#40;XMLA&#41;](xml-elements-commands/unlock-element-xmla.md)<br />-   [Actualizar elemento &#40;XMLA&#41;](xml-elements-commands/update-element-xmla.md)<br />-   [Elemento UpdateCells &#40;XMLA&#41;](xml-elements-commands/updatecells-element-xmla.md)|  
|Errores de la columna en conjuntos de filas tabulares|No se enumera en la especificación de XML for Analysis 1.1.|El [Error](xml-elements-properties/error-element-xmla.md) utiliza elemento [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para informar de errores para los elementos de la columna contenidos en un [fila](xml-elements-properties/error-element-xmla.md) elemento.|  
  
## <a name="see-also"></a>Vea también  
 [XML for Analysis &#40;XMLA&#41; referencia](xml-for-analysis-xmla-reference.md)  
  
  
