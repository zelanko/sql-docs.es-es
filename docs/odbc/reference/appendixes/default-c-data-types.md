---
title: Tipos de datos de C predeterminados | Microsoft Docs
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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307056"
---
# <a name="default-c-data-types"></a>Tipos de datos predeterminados de C
Si una aplicación especifica SQL_C_DEFAULT en **SQLBindCol**, **SQLGetData**o **SQLBindParameter**, el controlador supone que el tipo de datos C del búfer de entrada o de salida corresponde al tipo de datos SQL de la columna o parámetro al que está enlazado el búfer.  
  
> [!IMPORTANT]  
>  Las aplicaciones interoperables no deben utilizar SQL_C_DEFAULT. En su lugar, siempre deben especificar el tipo C del búfer que están usando. Esto se debe a que los controladores no siempre determinan correctamente el tipo C predeterminado, por las razones siguientes:  
  
-   Si el DBMS promueve un tipo de datos SQL de una columna o parámetro, el controlador no puede determinar el tipo de datos SQL original de una columna o parámetro. Por lo tanto, no puede determinar el tipo de datos de C predeterminado correspondiente.  
  
-   Si el controlador no puede determinar si una columna o un parámetro determinados están firmados, como suele ser el caso cuando lo controla el DBMS, el controlador no puede determinar si el tipo de datos de C predeterminado correspondiente debe estar firmado o sin firmar.  
  
     Dado que SQL_C_DEFAULT se proporciona solo como una comodidad de programación, la aplicación no pierde ninguna funcionalidad cuando especifica el tipo de datos real de C.  
  
 En este apéndice se incluye una tabla que muestra el tipo de datos de C predeterminado para cada tipo de [datos de SQL](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).
