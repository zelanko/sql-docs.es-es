---
title: ISSCommandWithParameters (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSCommandWithParameters (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSCommandWithParameters interface
ms.assetid: 3419b7f3-36a3-4863-816e-e641e4e90496
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4de7c6a99afcbd7db7c6e233fb737f129b536b8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63209768"
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
  **ISSCommandWithParameters** expone la compatibilidad con los tipos XML y definidos por el usuario (UDT) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ésta es una interfaz opcional que hereda de la interfaz OLE DB **ICommandWithParameters**básica. Además de los tres métodos heredados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**y **SetParameterInfo**; **ISSCommandWithParameters** proporciona dos nuevos métodos que se utilizan para administrar tipos de datos específicos de servidor.  
  
> [!NOTE]  
>  La interfaz **ISSCommandWithParameters** se puede utilizar cuando se utilizan componentes de servicio, pero los propios componentes de servicio no utilizarán esta interfaz.  
  
|Método|Descripción|  
|------------|-----------------|  
|[Isscommandwithparameters:: Getparameterproperties &#40;OLE DB&#41;](isscommandwithparameters-getparameterproperties-ole-db.md)|Devuelve la estructura del conjunto de propiedades **SSPARAMPROPS** en la matriz de cada parámetro UDT o XML pasado al comando, pero no devuelve nada en los demás tipos de parámetros.|  
|[Isscommandwithparameters:: SetParameterProperties &#40;OLE DB&#41;](isscommandwithparameters-setparameterproperties-ole-db.md)|Establece las propiedades de parámetro por cada parámetro por ordinal o establece propiedades masivas de parámetro mediante la especificación de una matriz de estructuras **SSPARAMPROPS** .|  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [Utilizar tipos de datos XML](../native-client/features/using-xml-data-types.md)   
 [Usar tipos definidos por el usuario](../native-client/features/using-user-defined-types.md)  
  
  
