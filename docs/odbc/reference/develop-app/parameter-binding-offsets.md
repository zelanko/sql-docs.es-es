---
description: Desplazamientos de enlace de parámetros
title: Desplazamientos de enlaces de parámetros | Microsoft Docs
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
ms.openlocfilehash: 71b4958e77d01c613e33386ec1b2b21ed91f0a67
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476547"
---
# <a name="parameter-binding-offsets"></a>Desplazamientos de enlace de parámetros
Una aplicación puede especificar que se agregue un desplazamiento a las direcciones de búfer de parámetros enlazados y a las direcciones de búfer de indicador/longitud correspondientes cuando se llame a **SQLExecDirect** o **SQLExecute** . El resultado de estas adiciones determina las direcciones utilizadas en estas operaciones.  
  
 Los desplazamientos de enlace permiten a una aplicación cambiar los enlaces sin llamar a **SQLBindParameter** para los parámetros enlazados previamente. Una llamada a **SQLBindParameter** para volver a enlazar un parámetro cambia la dirección del búfer y el puntero de longitud/indicador. Al volver a enlazar con un desplazamiento, por otro lado, simplemente se agrega un desplazamiento a la dirección del búfer de parámetros enlazados existente y la dirección del búfer de indicador/longitud. Cuando se usan desplazamientos, los enlaces son una "plantilla" de cómo se colocan los búferes de la aplicación y la aplicación puede moverla a distintas áreas de memoria cambiando el desplazamiento. Se puede especificar un nuevo desplazamiento en cualquier momento y siempre se agrega a los valores enlazados originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción SQL_ATTR_PARAM_BIND_OFFSET_PTR en la dirección de un búfer SQLINTEGER donde. Antes de que la aplicación llame a una función que utiliza los enlaces, coloca un desplazamiento en bytes en este búfer, siempre que la dirección del búfer de parámetros o la dirección del búfer de longitud/indicador sea 0, y el parámetro enlazado esté en la instrucción SQL. La suma de la dirección y el desplazamiento debe ser una dirección válida. (Esto significa que el desplazamiento y la dirección a la que se agrega el desplazamiento pueden ser no válidos, siempre que su suma sea una dirección válida).  
  
> [!NOTE]  
>  Los desplazamientos de enlace no son compatibles con ODBC 2. Controladores *x* .
