---
title: ICommandWithParameters | Microsoft Docs
description: Interfaz ICommandWithParameters
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 7194b886ed972937c30b775bb6ec093e1b4fe612
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66790614"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Mejoras en el principio del motor de base de datos con [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permitir ICommandWithParameters:: GetParameterInfo obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por CommandWithParameters::GetParameterInfo en versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Detección de metadatos](../../oledb/features/metadata-discovery.md).  
  
 También a partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], al llamar a ICommandWithParameters::SetParameterInfo, el último valor pasado al parámetro *pwszName* debe ser un identificador válido. Para obtener más información, vea [Database Identifiers](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
