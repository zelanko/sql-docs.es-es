---
title: Tipos de datos C predeterminados | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c4147b1bfa5ffb1e379c3aa8be2c9ea2a9d2775
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47854113"
---
# <a name="default-c-data-types"></a>Tipos de datos predeterminados de C
Si una aplicación especifica SQL_C_DEFAULT en **SQLBindCol**, **SQLGetData**, o **SQLBindParameter**, el controlador se da por supuesto que el C tipo de datos del búfer de entrada o salida corresponde al tipo de datos SQL de la columna o parámetro al que está enlazado el búfer.  
  
> [!IMPORTANT]  
>  Aplicaciones interoperables no deberían utilizar SQL_C_DEFAULT. En su lugar, debe especificar siempre el tipo C de búfer que se usan. Esto es porque los controladores siempre correctamente no pueden determinar el tipo C de forma predeterminada, por las razones siguientes:  
  
-   Si el DBMS promueve a un tipo de datos SQL de una columna o parámetro, el controlador no puede determinar el tipo de datos SQL original de una columna o parámetro. Por lo tanto, no puede determinar el tipo de datos de C predeterminado correspondiente.  
  
-   Si el controlador no puede determinar si una determinada columna o parámetro está firmado, como suele ocurrir cuando se trata de controlan el DBMS, el controlador no puede determinar si tipo de datos C predeterminado correspondientes debe ser con o sin signo.  
  
     Porque SQL_C_DEFAULT se proporciona sólo como una comodidad en la programación, la aplicación no pierda ninguna funcionalidad cuando especifica el tipo de datos C real.  
  
 Una tabla que muestra el tipo de datos C predeterminado para cada tipo de datos SQL se incluye en [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md), más adelante en este apéndice.
