---
title: Especificación de un elemento raíz para usarlo con FOR XML | Microsoft Docs
description: Vea una consulta de ejemplo que especifica la opción ROOT de la cláusula FOR XML para solicitar un solo elemento de nivel superior en el XML resultante.
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying root element example
- RAW mode, with FOR XML example
ms.assetid: bcc54b11-0713-4e43-8dbe-d6f3ad1993b5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: cf32be608e844036893b7c7dbf42ba76db0c203f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632650"
---
# <a name="example-specifying-a-root-element-for-the-xml-generated-by-for-xml"></a>Ejemplo: Especificación de un elemento raíz para el XML generado por FOR XML
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Al especificar la opción `ROOT` en la consulta `FOR XML` , puede solicitar un solo elemento de nivel superior para el XML resultante, como se muestra en esta consulta. El argumento especificado para la directiva `ROOT` proporciona el nombre del elemento raíz.  
  
## <a name="example"></a>Ejemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119 or ProductModelID=115  
FOR XML RAW, ROOT('MyRoot')  
GO
```  
  
 El resultado es el siguiente:  
  
```  
<MyRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
  <row ProductModelID="115" Name="Cable Lock" />  
</MyRoot>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
