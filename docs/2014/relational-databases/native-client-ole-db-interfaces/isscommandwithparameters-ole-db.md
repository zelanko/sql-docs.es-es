---
title: ISSCommandWithParameters (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ceca46260d82cc6f9a179a642821aee55e57d6e3
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429994"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters** expone la compatibilidad para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] XML y tipos definidos por el usuario (UDT). Ésta es una interfaz opcional que hereda de la interfaz OLE DB **ICommandWithParameters**básica. Además de los tres métodos heredados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**y **SetParameterInfo**; **ISSCommandWithParameters** proporciona dos nuevos métodos que se utilizan para administrar tipos de datos específicos de servidor.  
  
> [!NOTE]  
>  La interfaz **ISSCommandWithParameters** se puede utilizar cuando se utilizan componentes de servicio, pero los propios componentes de servicio no utilizarán esta interfaz.  
  
|Método|Descripción|  
|------------|-----------------|  
|[Isscommandwithparameters:: Getparameterproperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|Devuelve la estructura del conjunto de propiedades **SSPARAMPROPS** en la matriz de cada parámetro UDT o XML pasado al comando, pero no devuelve nada en los demás tipos de parámetros.|  
|[Isscommandwithparameters:: SetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|Establece las propiedades de parámetro por cada parámetro por ordinal o establece propiedades masivas de parámetro mediante la especificación de una matriz de estructuras **SSPARAMPROPS** .|  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [Uso de tipos de datos XML](../native-client/features/using-xml-data-types.md)   
 [Usar tipos definidos por el usuario](../native-client/features/using-user-defined-types.md)  
  
  
