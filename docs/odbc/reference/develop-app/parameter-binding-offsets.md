---
title: Desplazamientos de enlace de parámetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1fd069336a52b0a27ae927880f749c02d2c1d43
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765902"
---
# <a name="parameter-binding-offsets"></a>Desplazamientos de enlace de parámetros
Una aplicación puede especificar que se agrega un desplazamiento que va a enlazar las direcciones de búfer de parámetro y el indicador de longitud correspondiente direcciones de búfer cuando **SQLExecDirect** o **SQLExecute** se llama. El resultado de estas adiciones determina las direcciones usadas en estas operaciones.  
  
 Desplazamientos de enlace permite que una aplicación cambiar los enlaces sin llamar a **SQLBindParameter** para parámetros enlazados previamente. Una llamada a **SQLBindParameter** para volver a enlazar un parámetro cambia la dirección del búfer y el puntero de longitud/indicador. Volver a enlazar con un desplazamiento, por otro lado, simplemente agrega un desplazamiento a la dirección de búfer de parámetros enlazados existente y búfer indicador de longitud. Cuando se utilizan los desplazamientos, los enlaces son una "plantilla" de la disposición de los búferes de la aplicación y la aplicación puede mover esta "plantilla" a diferentes áreas de memoria cambiando el desplazamiento. Un nuevo desplazamiento puede especificarse en cualquier momento y siempre se agrega a los valores enlazados originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción SQL_ATTR_PARAM_BIND_OFFSET_PTR a la dirección de un búfer SQLINTEGER. Antes de la aplicación llama a una función que usa los enlaces, coloca un desplazamiento en bytes de este búfer, siempre que la dirección del búfer de parámetro ni la dirección del búfer de longitud/indicador es 0 y el parámetro dependiente está en la instrucción SQL. La suma de la dirección y el desplazamiento debe ser una dirección válida. (Esto significa que uno o ambos el desplazamiento y la dirección a la que se agrega el desplazamiento pueden ser válidos, siempre y cuando su suma es una dirección válida.)  
  
> [!NOTE]  
>  No se admiten los desplazamientos de enlace por ODBC 2. *x* controladores.
