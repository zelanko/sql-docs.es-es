---
title: Desplazamientos de enlace de parámetros ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de67b230883f3cf8a582e73ce82e8c4bd7d21ad0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282504"
---
# <a name="parameter-binding-offsets"></a>Desplazamientos de enlace de parámetros
Una aplicación puede especificar que se agrega un desplazamiento a las direcciones de búfer de parámetros enlazados y las direcciones de búfer de longitud/indicador correspondientes cuando se llama a **SQLExecDirect** o **SQLExecute.** El resultado de estas adiciones determina las direcciones utilizadas en estas operaciones.  
  
 Los desplazamientos de enlace permiten a una aplicación cambiar los enlaces sin llamar a **SQLBindParameter** para los parámetros enlazados anteriormente. Una llamada a **SQLBindParameter** para volver a enlazar un parámetro cambia la dirección del búfer y el puntero de longitud/indicador. Por otro lado, el reenlace con un desplazamiento simplemente agrega un desplazamiento a la dirección de búfer de parámetro enlazada existente y a la dirección de búfer de longitud/indicador. Cuando se utilizan desplazamientos, los enlaces son una "plantilla" de cómo se distribuyen los búferes de aplicación y la aplicación puede mover esta "plantilla" a diferentes áreas de memoria cambiando el desplazamiento. Se puede especificar un nuevo desplazamiento en cualquier momento y siempre se agrega a los valores enlazados originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción SQL_ATTR_PARAM_BIND_OFFSET_PTR en la dirección de un búfer SQLINTEGER. Antes de que la aplicación llame a una función que usa los enlaces, coloca un desplazamiento en bytes en este búfer, siempre y cuando ni la dirección del búfer de parámetro ni la dirección del búfer de longitud/indicador sea 0, y el parámetro enlazado está en la instrucción SQL. La suma de la dirección y el desplazamiento debe ser una dirección válida. (Esto significa que el desplazamiento o ambos y la dirección a la que se agrega el desplazamiento pueden ser inválidos, siempre y cuando su suma sea una dirección válida.)  
  
> [!NOTE]  
>  ODBC 2 no admite los desplazamientos de enlace. *x* controladores.
