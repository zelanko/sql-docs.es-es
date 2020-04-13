---
title: Compatibilidad de FOR XML con los tipos de datos definidos por el usuario (UDT) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- UDTs [SQL Server], XML
- user-defined types [SQL Server], XML
ms.assetid: 354e2150-fa2a-4583-b1aa-6b78ae4378b6
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 371e3e4070b7a167a69ebd0df39be82686f824c9
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "80665329"
---
# <a name="for-xml-support-for-the-user-defined-data-types-udt"></a>Compatibilidad de FOR XML con los tipos de datos definidos por el usuario (UDT)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  FOR XML no admite los tipos de datos definidos por el usuario (UDT) CLR (Common Language Runtime).  
  
 Para usar FOR XML con tipos de datos definidos por el usuario CLR, asegúrese de que el tipo de datos tiene una serialización XML y use una conversión explícita a XML en la cláusula SELECT FOR XML.  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad de FOR XML con varios tipos de datos de SQL Server](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
