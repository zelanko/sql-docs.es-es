---
title: Parámetro de enlace desplazamientos | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2d5228c7ce920eb56b0b947784b3d5a7bb2d6266
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="parameter-binding-offsets"></a>Desplazamientos de enlace de parámetros
Una aplicación puede especificar que se ha agregado un desplazamiento a direcciones de búfer de parámetro y el indicador de longitud correspondiente enlazados búfer direcciones cuando **SQLExecDirect** o **SQLExecute** se llama. El resultado de estas adiciones determina las direcciones usadas en estas operaciones.  
  
 Desplazamientos de enlace permiten que una aplicación cambiar los enlaces sin llamar a **SQLBindParameter** para parámetros enlazados previamente. Una llamada a **SQLBindParameter** volver a enlazar un parámetro cambia la dirección del búfer y el puntero de longitud/indicador. Volver a enlazar con un desplazamiento, por otro lado, simplemente agrega un desplazamiento a la dirección de búferes de parámetros enlazados existente y la dirección del búfer de longitud/indicador. Cuando se utilizan los desplazamientos, los enlaces son "plantilla" de cómo se distribuyen los búferes de la aplicación y la aplicación puede mover esta "plantilla" a diferentes áreas de memoria cambiando el desplazamiento. Un desplazamiento nuevo puede especificarse en cualquier momento y siempre se agrega a los valores enlazados originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción de SQL_ATTR_PARAM_BIND_OFFSET_PTR a la dirección de un búfer SQLINTEGER. Antes de que la aplicación llama a una función que utiliza los enlaces, coloca un desplazamiento en bytes de este búfer, siempre y cuando la dirección del búfer de parámetro ni la dirección de búfer de longitud/indicador es 0 y el parámetro dependiente está en la instrucción SQL. La suma de la dirección y el desplazamiento debe ser una dirección válida. (Esto significa que uno o ambos el desplazamiento y la dirección a la que se agrega el desplazamiento pueden ser válidos, como la suma es una dirección válida.)  
  
> [!NOTE]  
>  Desplazamientos de enlace no son compatibles con ODBC 2. *x* controladores.
