---
title: ISSCommandWithParameters (OLE DB) | Documentos de Microsoft
description: ISSCommandWithParameters (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSCommandWithParameters (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSCommandWithParameters interface
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fd350eb8c63a95d0ba64950be2ab689696fef0e5
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="isscommandwithparameters-ole-db"></a>ISSCommandWithParameters (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSCommandWithParameters** interfaz expone la compatibilidad para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] XML y tipos definidos por el usuario (UDT). Es una interfaz opcional que hereda de la interfaz de OLE DB **ICommandWithParameters**. Además de los tres métodos heredados de **ICommandWithParameters**; **GetParameterInfo**, **MapParameterNames**, y **SetParameterInfo**; **ISSCommandWithParameters** proporciona dos nuevos métodos que se utilizan para controlar los tipos de datos específicos del servidor.  
  
> [!NOTE]  
>  El **ISSCommandWithParameters** interfaz se puede usar cuando se utilizan componentes de servicio, pero los componentes del servicio no usará esta interfaz.  
  
|Método|Description|  
|------------|-----------------|  
|[Isscommandwithparameters:: Getparameterproperties &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-getparameterproperties-ole-db.md)|Devuelve la estructura del conjunto de propiedades **SSPARAMPROPS** en la matriz de cada parámetro UDT o XML pasado al comando, pero no devuelve nada en los demás tipos de parámetros.|  
|[Isscommandwithparameters:: SetParameterProperties &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/isscommandwithparameters-setparameterproperties-ole-db.md)|Establece las propiedades de parámetro por cada parámetro por ordinal o establece propiedades masivas de parámetro mediante la especificación de una matriz de estructuras **SSPARAMPROPS** .|  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40; OLE DB &#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [Uso de tipos de datos XML](../../oledb/features/using-xml-data-types.md)   
 [Usar tipos definidos por el usuario](../../oledb/features/using-user-defined-types.md)  
  
  
