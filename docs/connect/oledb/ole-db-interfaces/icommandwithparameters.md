---
title: ICommandWithParameters (controlador OLE DB) | Microsoft Docs
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
ms.openlocfilehash: afb49ad0dd1d1bf6275fb093b42c97e34cb7d670
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244496"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Las mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] permiten a ICommandWithParameters::GetParameterInfo obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores que devuelve CommandWithParameters::GetParameterInfo en las versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Detección de metadatos](../../oledb/features/metadata-discovery.md).  
  
 También a partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], al llamar a ICommandWithParameters::SetParameterInfo, el último valor pasado al parámetro *pwszName* debe ser un identificador válido. Para obtener más información, vea [Database Identifiers](../../../relational-databases/databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
