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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 25156dd240c90b7cc50cc44fba90125f5c6eab85
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702711"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>Compatibilidad de FOR XML con los tipos de datos definidos por el usuario (UDT)
  FOR XML no admite los tipos de datos definidos por el usuario (UDT) CLR (Common Language Runtime).  
  
 Para usar FOR XML con tipos de datos definidos por el usuario CLR, asegúrese de que el tipo de datos tiene una serialización XML y use una conversión explícita a XML en la cláusula SELECT FOR XML.  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad de FOR XML con varios tipos de datos de SQL Server](for-xml-support-for-various-sql-server-data-types.md)  
  
  
