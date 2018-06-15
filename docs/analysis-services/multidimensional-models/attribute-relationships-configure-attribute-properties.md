---
title: Configurar propiedades de relación de atributo | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9a7270dd698dfb8d3d3002c302186e97b912044f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023152"
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
  
  
