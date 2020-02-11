---
title: ICommandWithParameters | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 66644c70-def7-46d8-8c47-b883292a0288
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ea85e526d99e586c2534eee8ab83c6ddc66939db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62643253"
---
# <a name="icommandwithparameters"></a>ICommandWithParameters
  Las mejoras en el motor de base [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] de datos a partir de permiten ICommandWithParameters:: GetParameterInfo para obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por CommandWithParameters:: GetParameterInfo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en versiones anteriores de. Para obtener más información, vea [Detección de metadatos](../native-client/features/metadata-discovery.md).  
  
 También a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], al llamar a ICommandWithParameters::SetParameterInfo, el último valor pasado al parámetro *pwszName* debe ser un identificador válido. Para obtener más información, vea [Database Identifiers](../databases/database-identifiers.md).  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
