---
title: Compatibilidad de FOR XML con los tipos de datos definidos por el usuario (UDT) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 553010f85d07eb922d7644ef91504c55a1367ee0
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>Compatibilidad de FOR XML con los tipos de datos definidos por el usuario (UDT)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] FOR XML no admite los tipos de datos definidos por el usuario (UDT) de Common Language Runtime (CLR).  
  
 Para usar FOR XML con tipos de datos definidos por el usuario CLR, asegúrese de que el tipo de datos tiene una serialización XML y use una conversión explícita a XML en la cláusula SELECT FOR XML.  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con FOR XML para varios tipos de datos de SQL Server](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
