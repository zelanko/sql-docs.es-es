---
title: Ejemplos de expresiones avanzadas de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [Integration Services]
- operators [Integration Services]
- expressions [Integration Services], examples
- examples [Integration Services]
ms.assetid: c7794ba3-0de5-466b-ae8a-9ddd27360049
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 1476a0ec94f733983bffb9dee36bed6efd0e4b59
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35334139"
---
# <a name="examples-of-advanced-integration-services-expressions"></a>Ejemplos de expresiones avanzadas de Integration Services
  Esta sección proporciona ejemplos de expresiones avanzadas que combinan varios operadores y varias funciones. Si se usa una expresión en una restricción de precedencia o en la transformación División condicional, su evaluación debe devolver un valor booleano. Sin embargo, esta restricción no se aplica a las expresiones usadas en expresiones de propiedades, variables, la transformación Columna derivada o el contenedor de bucles For.  
  
 En los siguientes ejemplos se usa la base de datos **AdventureWorks** y la base de datos [!INCLUDE[ssSampleDBDWobject](../../includes/sssampledbdwobject-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cada ejemplo identifica las tablas que utiliza.  
  
## <a name="boolean-expressions"></a>Expresiones booleanas  
  
-   En este ejemplo se utiliza la tabla **Product** . La evaluación de la expresión busca la entrada del mes en la columna **SellStartDate** y devuelve TRUE si el mes es junio o un mes posterior.  
  
    ```  
    DATEPART("mm",SellStartDate) > 6  
    ```  
  
-   En este ejemplo se utiliza la tabla **Product** . La expresión evalúa el resultado redondeado de dividir la columna **ListPrice** por la columna **StandardCost** y devuelve TRUE si el resultado es mayor que 1,5.  
  
    ```  
    ROUND(ListPrice / StandardCost,2) > 1.50  
    ```  
  
-   En este ejemplo se utiliza la tabla **Product** . La expresión devuelve TRUE si las tres operaciones devuelven TRUE. Si la columna **Size** y la variable **BikeSize** tienen tipos de datos incompatibles, la expresión requiere una conversión explícita, como se indica en el segundo ejemplo. La conversión a DT_WSTR incluye la longitud de la cadena.  
  
    ```  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE && Size != @BikeSize  
    MakeFlag ==  TRUE && FinishedGoodsFlag == TRUE  && Size != (DT_WSTR,10)@BikeSize  
    ```  
  
-   En este ejemplo se utiliza la tabla **CurrencyRate** . La expresión compara valores de tablas y variables. Devuelve TRUE si las entradas de la columna **FromCurrencyCode** o **ToCurrencyCode** son iguales a los valores de la variable y si el valor de **AverageRate** es mayor que el valor de **EndOfDayRate**.  
  
    ```  
    (FromCurrencyCode == @FromCur || ToCurrencyCode == @ToCur) && AverageRate > EndOfDayRate  
    ```  
  
-   En este ejemplo se utiliza la tabla **Currency** . La expresión devuelve TRUE si el primer carácter de la columna **Name** no es a o A.  
  
    ```  
    SUBSTRING(UPPER(Name),1,1) != "A"  
    ```  
  
     La siguiente expresión proporciona los mismos resultados, pero es mucho más eficaz porque solo se convierte a mayúsculas un carácter.  
  
    ```  
    UPPER(SUBSTRING(Name,1,1)) != "A"  
    ```  
  
## <a name="non-boolean-expressions"></a>Expresiones no booleanas  
 Las expresiones no booleanas se usan en la transformación Columna derivada, en expresiones de propiedades y en el contenedor de bucles For.  
  
-   En este ejemplo se utiliza la tabla **Contact** . La expresión quita los espacios iniciales y finales de las columnas **FirstName**, **MiddleName**y **LastName** . Extrae la primera letra de la columna **MiddleName** si no es NULL, concatena la inicial del segundo nombre y los valores de **FirstName** y **LastName**, e inserta los espacios apropiados entre los valores.  
  
    ```  
    TRIM(FirstName) + " " + (!ISNULL(MiddleName) ? SUBSTRING(MiddleName,1,1) + " " : "") + TRIM(LastName)  
    ```  
  
-   En este ejemplo se utiliza la tabla **Contact** . La expresión valida las entradas de la columna **Salutation** . Devuelve una entrada **Salutation** o una cadena vacía.  
  
    ```  
    (Salutation == "Sr." || Salutation == "Ms." || Salutation == "Sra." || Salutation == "Mr.") ? Salutation : ""  
    ```  
  
-   En este ejemplo se utiliza la tabla **Product** . La expresión convierte el primer carácter de la columna **Color** a mayúsculas y convierte los demás caracteres a minúsculas.  
  
    ```  
    UPPER(SUBSTRING(Color,1,1)) + LOWER(SUBSTRING(Color,2,15))  
    ```  
  
-   En este ejemplo se utiliza la tabla **Product** . La expresión calcula el número de meses que se ha vendido un producto y devuelve la cadena "Unknown" si la columna **SellStartDate** o **SellEndDate** contiene NULL.  
  
    ```  
    !(ISNULL(SellStartDate)) && !(ISNULL(SellEndDate)) ? (DT_WSTR,2)DATEDIFF("mm",SellStartDate,SellEndDate) : "Unknown"  
    ```  
  
-   En este ejemplo se utiliza la tabla **Product** . La expresión calcula el margen de beneficio de la columna **StandardCost** y redondea el resultado a una precisión de dos. El resultado se presenta como un porcentaje.  
  
    ```  
    ROUND(ListPrice / StandardCost,2) * 100  
    ```  
  
## <a name="related-tasks"></a>Related Tasks  
 [utilizar una expresión en un componente de flujo de datos](http://msdn.microsoft.com/library/9181b998-d24a-41fb-bb3c-14eee34f910d)  
  
## <a name="related-content"></a>Contenido relacionado  
 Artículo técnico, sobre la [referencia rápida de expresiones de SSIS](http://go.microsoft.com/fwlink/?LinkId=746575), en pragmaticworks.com  
  
  
