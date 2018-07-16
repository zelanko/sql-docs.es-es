---
title: Comandos (XMLA) | Microsoft Docs
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
topic_type:
- apiref
- apinav
helpviewer_keywords:
- commands [XML for Analysis]
- XML for Analysis, commands
- XMLA, commands
ms.assetid: c8a93ea6-8eb5-4204-b037-69cb442a0082
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 215db39cdf87cff69f2bfefbc28e730590daec15
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298895"
---
# <a name="commands-xmla"></a>Comandos (XMLA)
  Esta sección de referencia contiene elementos de XML for Analysis (XMLA) que se pueden utilizar dentro del elemento `Command` durante una llamada al método `Execute`.  
  
|Elemento|Descripción|  
|-------------|-----------------|  
|[Elemento Alter (XMLA)](alter-element-xmla.md)|Contiene elementos de Analysis Services Scripting Language (ASSL) utilizados por el [Execute](../xml-elements-methods-execute.md) método para modificar objetos en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento Backup](backup-element-xmla.md)|Realiza copias de seguridad un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] base de datos a un archivo de copia de seguridad.|  
|[Elemento Batch](batch-element-xmla.md)|Realiza una o varias de XML para los comandos de Analysis (XMLA) como una operación por lotes, secuencialmente o en paralelo, en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Elemento BeginTransaction](begintransaction-element-xmla.md)|Comienza una transacción en la sesión actual con una instancia de Analysis Services.|  
|[Elemento Cancel](cancel-element-xmla.md)|Cancela un comando actualmente en ejecución en una instancia de Analysis Services.|  
|[Elemento ClearCache](clearcache-element-xmla.md)|Borra la memoria caché para el objeto especificado en una instancia de Analysis Services.|  
|[Elemento CommitTransaction](committransaction-element-xmla.md)|Confirma una transacción en la sesión actual con una instancia de Analysis Services.|  
|[Elemento Create](create-element-xmla.md)|Contiene elementos de Analysis Services Scripting Language (ASSL) utilizados por el [Execute](../xml-elements-methods-execute.md) método para crear objetos en una instancia de Analysis Services.|  
|[Elemento Delete](delete-element-xmla.md)|Elimina un objeto en una instancia de Analysis Services.|  
|[Elemento DesignAggregations](designaggregations-element-xmla.md)|Crea agregaciones para un diseño de agregaciones en una a instancia de Analysis Services.|  
|[Elemento Drop](drop-element-xmla.md)|Elimina miembros de atributo de una dimensión.|  
|[Elemento Insert](insert-element-xmla.md)|Inserta miembros de atributo en una dimensión.|  
|[Elemento Lock](lock-element-xmla.md)|Bloquea un objeto especificado en una instancia de Analysis Services.|  
|[Elemento MergePartitions](mergepartitions-element-xmla.md)|Combina los datos de una o varias particiones de origen en una partición de destino y, a continuación, eliminan las particiones de origen.|  
|[Elemento NotifyTableChange](notifytablechange-element-xmla.md)|Notifica a una instancia de Analysis Services que se ha producido un cambio en las tablas de un origen de datos especificado.|  
|[Elemento Process](process-element-xmla.md)|Procesa objetos en una instancia de Analysis Services.|  
|[Elemento Restore](restore-element-xmla.md)|Restaura una base de datos de Analysis Services desde un archivo de copia de seguridad.|  
|[Elemento RollbackTransaction](rollbacktransaction-element-xmla.md)|Revierte una transacción en la sesión actual con una instancia de Analysis Services.|  
|[Elemento Statement](statement-element-xmla.md)|Contiene una consulta o instrucción se envíe mediante la [Execute](../xml-elements-methods-execute.md) método a una instancia de Analysis Services.|  
|[Elemento Subscribe](subscribe-element-xmla.md)|Suscribe a un seguimiento y devuelve un conjunto de filas que contiene los eventos de seguimiento de una instancia de Analysis Services.|  
|[Elemento Synchronize](synchronize-element-xmla.md)|Sincroniza una base de datos de Analysis Services con otra base de datos existente.|  
|[Elemento Unlock](unlock-element-xmla.md)|Desbloquea un bloqueo especificado en una instancia de Analysis Services.|  
|[Elemento Update](../xml-elements-commands/update-element-xmla.md)|Actualiza miembros de atributo de una dimensión.|  
|[Elemento UpdateCells](updatecells-element-xmla.md)|Actualiza las celdas en un cubo habilitado para escritura.|  
  
  
