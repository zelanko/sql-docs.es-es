---
title: Compatibilidad de FOR XML con los tipos de datos definidos por el usuario (UDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 275c6a13b0351bfa95e3d9ac642b1300f88e5c22
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48086185"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>Compatibilidad de FOR XML con los tipos de datos definidos por el usuario (UDT)
  FOR XML no admite los tipos de datos definidos por el usuario (UDT) CLR (Common Language Runtime).  
  
 Para usar FOR XML con tipos de datos definidos por el usuario CLR, asegúrese de que el tipo de datos tiene una serialización XML y use una conversión explícita a XML en la cláusula SELECT FOR XML.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con FOR XML para varios tipos de datos de SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  
