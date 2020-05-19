---
title: ICommandWithParameters | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 281abeeb0a29ba697fe8c8b42027280377315e86
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704863"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  Las mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permiten a ICommandWithParameters::GetParameterInfo obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores que devuelve CommandWithParameters::GetParameterInfo en las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Detección de metadatos](../native-client/features/metadata-discovery.md).  
  
 También a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], al llamar a ICommandWithParameters::SetParameterInfo, el último valor pasado al parámetro *pwszName* debe ser un identificador válido. Para obtener más información, vea [Database Identifiers](../databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
