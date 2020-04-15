---
title: SQL_ARD_TYPE Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], SQL_ARD_TYPE
- SQL_ARD_TYPE [ODBC]
ms.assetid: 8d87ca10-f955-4284-8689-e9f4cc31e7ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d7e28d6babb7db8364697ae62092256396b44914
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305036"
---
# <a name="sql_ard_type"></a>SQL_ARD_TYPE
El identificador de tipo SQL_ARD_TYPE se utiliza para indicar que los datos de un búfer serán del tipo especificado en el campo SQL_DESC_CONCISE_TYPE de la ARD. SQL_ARD_TYPE se especifica en el *TargetType* argumento de una llamada a **SQLGetData** en lugar de un tipo de datos específico y permite a una aplicación cambiar el tipo de datos del búfer cambiando el campo descriptor. Este valor vincula el * \** tipo de datos del búfer TargetValuePtr al campo descriptor. (SQL_ARD_TYPE no se especifica en una llamada a **SQLBindCol** o **SQLBindParameter** porque el tipo del búfer enlazado ya está vinculado a los campos SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE y se puede cambiar en cualquier momento cambiando cualquiera de esos campos.)  
  
 El identificador de tipo SQL_ARD_TYPE se puede utilizar para especificar valores no predeterminados para la precisión inicial y la precisión de segundos de los tipos de datos de intervalo, y los valores de precisión y escala para el tipo de datos SQL_C_NUMERIC. Para obtener más información, consulte Invalidación de la precisión predeterminada [de interlineado y segundos para](../../../odbc/reference/appendixes/overriding-default-leading-and-seconds-precision-for-interval-data-types.md) los tipos de datos de intervalo y [la precisión y escala predeterminadas para](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)tipos de datos numéricos, más adelante en este apéndice.
