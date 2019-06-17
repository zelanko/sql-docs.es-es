---
title: Descripciones de parámetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bc752afc0cb5214e629a343c35464e612b57c36
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049845"
---
# <a name="describing-parameters"></a>Descripciones de parámetros
**SQLBindParameter** tiene argumentos que describen el parámetro: el tipo SQL, precisión y escala. El controlador utiliza esta información, o *metadatos,* para convertir el valor del parámetro al tipo necesario para el origen de datos. A primera vista, puede parecer que el controlador está en una mejor posición para saber los metadatos de parámetros de la aplicación; Después de todo, el controlador puede detectar fácilmente los metadatos para un resultado de conjunto de columnas. Según parece, esto no es el caso. En primer lugar, la mayoría de los orígenes de datos no proporcionan una manera para el controlador detectar los metadatos del parámetro. Segundo, mayoría de las aplicaciones ya conoce los metadatos.  
  
 Si una instrucción SQL está codificado de forma rígida en la aplicación, el autor de la aplicación ya conoce el tipo de cada parámetro. Si se construye una instrucción SQL por la aplicación en tiempo de ejecución, la aplicación puede determinar los metadatos como si generara la instrucción. Por ejemplo, cuando la aplicación crea la cláusula  
  
```  
WHERE OrderID = ?  
```  
  
 puede llamar a **SQLColumns** para la columna OrderID.  
  
 La única situación en la que la aplicación no podrá determinar fácilmente los metadatos de parámetros es cuando el usuario escribe una instrucción con parámetros. En este caso, la aplicación llama a **SQLPrepare** para preparar la instrucción, **SQLNumParams** para determinar el número de parámetros, y **SQLDescribeParam** para describir cada parámetro. Sin embargo, como se mencionó anteriormente, la mayoría de los orígenes de datos no proporcionan una manera de detectar los metadatos del parámetro, por lo que el controlador **SQLDescribeParam** no se admite ampliamente.
