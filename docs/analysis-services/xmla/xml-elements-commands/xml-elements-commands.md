---
title: Comandos (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 644d4d443bf1731d03519141efc93f35f2eda4ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="xml-elements---commands"></a>Elementos XML - comandos
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Esta sección de referencia contiene XML para los elementos de Analysis (XMLA) que pueden utilizarse dentro de la **comando** elemento durante un **Execute** llamada al método.  
  
|Elemento|Description|  
|-------------|-----------------|  
|[Elemento ALTER (XMLA)](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)|Contiene elementos del Lenguaje de scripting de Analysis Services (ASSL) utilizados por el método [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) para modificar objetos en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento backup](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md)|Hace copia de seguridad de una base de datos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en un archivo de copia de seguridad.|  
|[Elemento por lotes](../../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md)|Realiza XML de uno o más para los comandos de Analysis (XMLA) como una operación por lotes, ya sea de forma secuencial o en paralelo, en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md)|Comienza una transacción en la sesión actual con una instancia de Analysis Services.|  
|[Elemento Cancel](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)|Cancela un comando actualmente en ejecución en una instancia de Analysis Services.|  
|[Elemento ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md)|Borra la memoria caché para el objeto especificado en una instancia de Analysis Services.|  
|[Elemento CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)|Confirma una transacción en la sesión actual con una instancia de Analysis Services.|  
|[Crear el elemento](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)|Contiene elementos de Analysis Services Scripting Language (ASSL) utilizados por el [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método para crear objetos en una instancia de Analysis Services.|  
|[Eliminar elemento](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md)|Elimina un objeto en una instancia de Analysis Services.|  
|[Elemento DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md)|Crea agregaciones para un diseño de agregaciones en una a instancia de Analysis Services.|  
|[Elemento DROP](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|Elimina miembros de atributo de una dimensión.|  
|[Elemento INSERT](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md)|Inserta miembros de atributo en una dimensión.|  
|[Elemento Lock](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)|Bloquea un objeto especificado en una instancia de Analysis Services.|  
|[Elemento MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|Combina los datos de una o varias particiones de origen en una partición de destino y, a continuación, eliminan las particiones de origen.|  
|[Elemento NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md)|Notifica a una instancia de Analysis Services que se ha producido un cambio en las tablas de un origen de datos especificado.|  
|[Elemento Process](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md)|Procesa objetos en una instancia de Analysis Services.|  
|[Elemento restore](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md)|Restaura una base de datos de Analysis Services desde un archivo de copia de seguridad.|  
|[Elemento RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)|Revierte una transacción en la sesión actual con una instancia de Analysis Services.|  
|[Elemento Statement](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)|Contiene una consulta o instrucción que se envíe mediante la [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método a una instancia de Analysis Services.|  
|[Elemento SUBSCRIBE](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md)|Suscribe a un seguimiento y devuelve un conjunto de filas que contiene los eventos de seguimiento de una instancia de Analysis Services.|  
|[Elemento Synchronize](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)|Sincroniza una base de datos de Analysis Services con otra base de datos existente.|  
|[Desbloquear elemento](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)|Desbloquea un bloqueo especificado en una instancia de Analysis Services.|  
|[Update (elemento)](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|Actualiza miembros de atributo de una dimensión.|  
|[Elemento UpdateCells](../../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)|Actualiza las celdas en un cubo habilitado para escritura.|  
  
  
