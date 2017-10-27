---
title: "Generar elementos para valores NULL mediante el parámetro XSINIL | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR XML clause, null values
- null values [SQL Server], XML
- ELEMENTS directive
- XSINIL parameter
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8484894ef6b6940952920532273955359f532795
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="generate-elements-for-null-values-with-the-xsinil-parameter"></a>Generar elementos para valores NULL mediante el parámetro XSINIL
  La directiva **ELEMENTS** genera XML en el cual cada valor de columna se asigna a un elemento del XML. Si el valor de la columna es NULL, no se agrega ningún elemento. Al especificar el parámetro **XSINIL** opcional en la directiva ELEMENTS, se puede solicitar que también se cree un elemento para el valor NULL. En este caso, se devuelve un elemento que tiene el atributo **xsi:nil** establecido en TRUE para cada valor de columna NULL.  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  

