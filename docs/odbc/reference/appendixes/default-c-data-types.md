---
title: Tipos de datos C predeterminados | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 83040ffdab8b9715fc8caeb024bec6a9fc05d4d4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="default-c-data-types"></a>Tipos de datos C predeterminado
Si una aplicación especifica SQL_C_DEFAULT en **SQLBindCol**, **SQLGetData**, o **SQLBindParameter**, el controlador da por hecho que los datos de C de tipo del búfer de entrada o salida se corresponde con el tipo de datos SQL de la columna o parámetro al que está enlazado el búfer.  
  
> [!IMPORTANT]  
>  Aplicaciones interoperables no deben utilizar SQL_C_DEFAULT. En su lugar, siempre debe especificar el tipo de C del búfer que están usando. Esto es porque controladores siempre correctamente no pueden determinar el tipo de C de forma predeterminada, por las razones siguientes:  
  
-   Si el DBMS promueve a un tipo de datos SQL de una columna o parámetro, el controlador no puede determinar el tipo de datos SQL original de una columna o parámetro. Por lo tanto, no puede determinar el tipo de datos de C predeterminado correspondiente.  
  
-   Si el controlador no puede determinar si una determinada columna o parámetro está firmado, como suele ocurrir cuando se trata de controlando el DBMS, el controlador no puede determinar si tipo de datos C predeterminado correspondientes debe ser con o sin signo.  
  
     Porque SQL_C_DEFAULT se proporciona únicamente como una comodidad en la programación, la aplicación no perderá ninguna funcionalidad cuando especifica el tipo de datos C real.  
  
 Se incluye una tabla que muestra el tipo de datos C predeterminado para cada tipo de datos SQL en [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md), más adelante en este apéndice.
