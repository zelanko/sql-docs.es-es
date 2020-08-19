---
description: Descripciones de parámetros
title: Describir parámetros | Microsoft Docs
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
ms.openlocfilehash: a41bee40403cc3562c41ccc13a15c706a0772e27
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476757"
---
# <a name="describing-parameters"></a>Descripciones de parámetros
**SQLBindParameter** tiene argumentos que describen el parámetro: su tipo SQL, precisión y escala. El controlador utiliza esta información, o *metadatos,* para convertir el valor del parámetro al tipo necesario para el origen de datos. A primera vista, podría parecer que el controlador está en una posición mejor para conocer los metadatos de los parámetros que la aplicación; después de todo, el controlador puede detectar fácilmente los metadatos de una columna de conjunto de resultados. Como resultó, no es así. En primer lugar, la mayoría de los orígenes de datos no proporcionan una manera para que el controlador detecte los metadatos de parámetros. En segundo lugar, la mayoría de las aplicaciones ya conocen los metadatos.  
  
 Si una instrucción SQL está codificada de forma rígida en la aplicación, el escritor de la aplicación ya conoce el tipo de cada parámetro. Si la aplicación crea una instrucción SQL en tiempo de ejecución, la aplicación puede determinar los metadatos a medida que compila la instrucción. Por ejemplo, cuando la aplicación construye la cláusula  
  
```  
WHERE OrderID = ?  
```  
  
 puede llamar a **SQLColumns** para la columna OrderID.  
  
 La única situación en la que la aplicación no puede determinar fácilmente los metadatos de parámetro es cuando el usuario escribe una instrucción con parámetros. En este caso, la aplicación llama a **SQLPrepare** para preparar la instrucción, **SQLNumParams** para determinar el número de parámetros y **SQLDescribeParam** para describir cada parámetro. Sin embargo, como se mencionó anteriormente, la mayoría de los orígenes de datos no proporcionan una manera para que el controlador detecte los metadatos de parámetros, por lo que **SQLDescribeParam** no se admite ampliamente.
