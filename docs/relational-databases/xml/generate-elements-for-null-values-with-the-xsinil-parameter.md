---
title: Generar elementos para valores NULL mediante el parámetro XSINIL | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0889de0a7525e0e5a7ea91ba169011aaf4e341a
ms.sourcegitcommit: 982a1dad0b58315cff7b54445f998499ef80e68d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66175178"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>Generar elementos para valores NULL mediante el parámetro XSINIL

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

La directiva **ELEMENTS** genera XML en el cual cada valor de columna se asigna a un elemento del XML. De forma predeterminada, si el valor de la columna es NULL, no se agrega ningún elemento. Pero al especificar el parámetro **XSINIL** opcional en la directiva ELEMENTS, se puede solicitar que también se cree un elemento para el valor NULL. En este caso, se devuelve un elemento que tiene el atributo **xsi:nil** establecido en TRUE para cada valor de columna NULL.  
  
## <a name="see-also"></a>Consulte también

[Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)

[SELECT: cláusula FOR](../../t-sql/queries/select-for-clause-transact-sql.md)
