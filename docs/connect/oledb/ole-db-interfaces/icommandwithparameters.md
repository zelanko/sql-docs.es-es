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
ms.openlocfilehash: 205a93fe5ce57a8b4c10fffb8648a1ef4c7b6506
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015460"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Las mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permiten a ICommandWithParameters::GetParameterInfo obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores que devuelve CommandWithParameters::GetParameterInfo en las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Detección de metadatos](../../oledb/features/metadata-discovery.md).  
  
 También a partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], al llamar a ICommandWithParameters::SetParameterInfo, el último valor pasado al parámetro *pwszName* debe ser un identificador válido. Para obtener más información, vea [Database Identifiers](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
