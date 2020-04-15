---
title: Descripción de los parámetros de la página de la página de la Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f4d9284294707da0a469bf75ff9812ad5f7855bb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305946"
---
# <a name="describing-parameters"></a>Descripciones de parámetros
**SQLBindParameter** tiene argumentos que describen el parámetro: su tipo SQL, precisión y escala. El controlador utiliza esta información, o *metadatos,* para convertir el valor del parámetro al tipo necesario para el origen de datos. A primera vista, puede parecer que el controlador está en una mejor posición para conocer los metadatos de parámetro que la aplicación; después de todo, el controlador puede descubrir fácilmente los metadatos de una columna de conjunto de resultados. Resulta que este no es el caso. En primer lugar, la mayoría de los orígenes de datos no proporcionan una manera para que el controlador detecte metadatos de parámetros. En segundo lugar, la mayoría de las aplicaciones ya conocen los metadatos.  
  
 Si una instrucción SQL está codificada de forma rígida en la aplicación, el escritor de aplicaciones ya conoce el tipo de cada parámetro. Si la aplicación construye una instrucción SQL en tiempo de ejecución, la aplicación puede determinar los metadatos a medida que compila la instrucción. Por ejemplo, cuando la aplicación construye la cláusula  
  
```  
WHERE OrderID = ?  
```  
  
 puede llamar a **SQLColumns** para la columna OrderID.  
  
 La única situación en la que la aplicación no puede determinar fácilmente los metadatos del parámetro es cuando el usuario escribe una instrucción parametrizada. En este caso, la aplicación llama a **SQLPrepare** para preparar la instrucción, **SQLNumParams** para determinar el número de parámetros y **SQLDescribeParam** para describir cada parámetro. Sin embargo, como se indicó anteriormente, la mayoría de los orígenes de datos no proporcionan una manera para que el controlador detecte metadatos de parámetros, por lo que **SQLDescribeParam** no es ampliamente compatible.
