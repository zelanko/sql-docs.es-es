---
title: Generación de elementos para valores NULL mediante XSINIL | Microsoft Docs
description: Obtenga información sobre cómo generar elementos XML para valores NULL mediante el parámetro XSINIL en la directiva ELEMENTS.
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
ms.custom: seo-lt-2019
ms.openlocfilehash: 7cf18eb7c5dea9a61988533205a3a64ab1ae3fd0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85638946"
---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>Generar elementos para valores NULL mediante el parámetro XSINIL

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

La directiva **ELEMENTS** genera XML en el cual cada valor de columna se asigna a un elemento del XML. De forma predeterminada, si el valor de la columna es NULL, no se agrega ningún elemento. Pero al especificar el parámetro **XSINIL** opcional en la directiva ELEMENTS, se puede solicitar que también se cree un elemento para el valor NULL. En este caso, se devuelve un elemento que tiene el atributo **xsi:nil** establecido en TRUE para cada valor de columna NULL.  
  
## <a name="see-also"></a>Consulte también

[Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)

[SELECT: cláusula FOR](../../t-sql/queries/select-for-clause-transact-sql.md)
