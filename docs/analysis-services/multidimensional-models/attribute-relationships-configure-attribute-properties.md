---
title: "Configurar propiedades de relación de atributo | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- flexible relationships (Analysis Services)
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
- properties [Analysis Services], attribute relationships
- rigid relationships (Analysis Services)
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bcc42c8bcd73c52851f3ed7fae5f4f7a4915b450
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="attribute-relationships---configure-attribute-properties"></a>Relaciones de atributo: configurar las propiedades de atributo
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
En la siguiente tabla se muestran y describen las propiedades de una relación de atributo.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|Atributo|Contiene el nombre del atributo.|  
|Cardinalidad|Indica la cardinalidad de la relación. Los valores son Many, para una relación de varios a uno, y One, para una relación de uno a uno. El valor predeterminado es Many. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], la propiedad de cardinalidad no tiene ningún efecto; su uso se reserva para una futura implementación.|  
|Nombre|Contiene el nombre descriptivo del atributo.|  
|RelationshipType|Indica si las relaciones de los miembros cambian a lo largo del tiempo. Los valores son Rigid, que significa que las relaciones entre los miembros no cambian a lo largo del tiempo, o Flexible, que significa que las relaciones entre los miembros sí cambian. El valor predeterminado es Flexible. Si define una relación como flexible, las agregaciones se quitan y se vuelven a calcular como parte de una actualización incremental (no se quitarán si solo se agregan miembros nuevos). Si define una relación como rígida, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retiene las agregaciones cuando la dimensión se actualiza de forma incremental. Si una relación definida como rígida cambia realmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] generará un error durante el procesamiento incremental. El rendimiento de la consulta y del procesamiento aumenta si se especifican las relaciones y las propiedades de relación apropiadas.|  
|Visible|Determina la visibilidad de la relación de los atributos. Los valores son True o False. El valor predeterminado es True.|  
  
  
