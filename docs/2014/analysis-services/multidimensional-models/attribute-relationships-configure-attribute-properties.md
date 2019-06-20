---
title: Configurar propiedades de relación de atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- flexible relationships (Analysis Services)
- attributes [Analysis Services], relationships
- relationships [Analysis Services], attributes
- properties [Analysis Services], attribute relationships
- rigid relationships (Analysis Services)
ms.assetid: fce511af-66d7-42fc-bb3a-6c516f16b10e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9a7cea5d2a08b31042ae3e2a07696cf63410d583
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077121"
---
# <a name="configure-attribute-relationship-properties"></a>Configurar propiedades de relación de los atributos
  En la siguiente tabla se muestran y describen las propiedades de una relación de atributo.  
  
|Property|Descripción|  
|--------------|-----------------|  
|Attribute|Contiene el nombre del atributo.|  
|Cardinalidad|Indica la cardinalidad de la relación. Los valores son Many, para una relación de varios a uno, y One, para una relación de uno a uno. El valor predeterminado es Many. En [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], la propiedad de cardinalidad no tiene ningún efecto; su uso se reserva para una futura implementación.|  
|NOMBRE|Contiene el nombre descriptivo del atributo.|  
|RelationshipType|Indica si las relaciones de los miembros cambian a lo largo del tiempo. Los valores son Rigid, que significa que las relaciones entre los miembros no cambian a lo largo del tiempo, o Flexible, que significa que las relaciones entre los miembros sí cambian. El valor predeterminado es Flexible. Si define una relación como flexible, las agregaciones se quitan y se vuelven a calcular como parte de una actualización incremental (no se quitarán si solo se agregan miembros nuevos). Si define una relación como rígida, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retiene las agregaciones cuando la dimensión se actualiza de forma incremental. Si una relación definida como rígida cambia realmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] generará un error durante el procesamiento incremental. El rendimiento de la consulta y del procesamiento aumenta si se especifican las relaciones y las propiedades de relación apropiadas.|  
|Visible|Determina la visibilidad de la relación de los atributos. Los valores son True o False. El valor predeterminado es True.|  
  
  
