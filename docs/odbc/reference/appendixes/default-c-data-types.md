---
title: Tipos de datos por defecto de C ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fdb787580e1c79df805f468416ab8993a1d32a26
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307056"
---
# <a name="default-c-data-types"></a>Tipos de datos predeterminados de C
Si una aplicación especifica SQL_C_DEFAULT en **SQLBindCol**, **SQLGetData**o **SQLBindParameter**, el controlador supone que el tipo de datos C del búfer de salida o entrada corresponde al tipo de datos SQL de la columna o parámetro al que está enlazado el búfer.  
  
> [!IMPORTANT]  
>  Las aplicaciones interoperables no deben utilizar SQL_C_DEFAULT. En su lugar, siempre deben especificar el tipo C del búfer que están utilizando. Esto se debe a que los controladores no siempre pueden determinar correctamente el tipo C predeterminado, por las siguientes razones:  
  
-   Si el DBMS promueve un tipo de datos SQL de una columna o parámetro, el controlador no puede determinar el tipo de datos SQL original de una columna o parámetro. Por lo tanto, no puede determinar el tipo de datos C predeterminado correspondiente.  
  
-   Si el controlador no puede determinar si una columna o parámetro determinado está firmado, como suele ocurrir cuando el DBMS lo controla, el controlador no puede determinar si el tipo de datos C predeterminado correspondiente debe estar firmado o sin firmar.  
  
     Dado que SQL_C_DEFAULT se proporciona solo como una conveniencia de programación, la aplicación no pierde ninguna funcionalidad cuando especifica el tipo de datos C real.  
  
 Una tabla que muestra el tipo de datos C predeterminado para cada tipo de datos SQL se incluye en Convertir datos de SQL a tipos de [datos C,](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)más adelante en este apéndice.
