---
title: Agregar atributos a dimensiones | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 80551dad-97ac-40d0-90af-b810780321ce
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 9e5a669c1e7db9624aa06ad35c593422dbb88ac0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="lesson-2-3---adding-attributes-to-dimensions"></a>Lección 2: 3: agregar atributos a dimensiones
Ahora que ha definido las dimensiones, puede rellenarlas con atributos que representan cada elemento de datos de la dimensión. Los atributos suelen estar basados en campos de una vista del origen de datos. Al agregar atributos a una dimensión, puede incluir campos de cualquier tabla de la vista del origen de datos.  
  
En esta tarea, usará el Diseñador de dimensiones para agregar atributos a las dimensiones Customer y Product. La dimensión Customer incluirá atributos basados en campos de las tablas Customer y Geography.  
  
## <a name="adding-attributes-to-the-customer-dimension"></a>Agregar atributos a la dimensión Customer  
  
#### <a name="to-add-attributes"></a>Para agregar atributos  
  
1.  Abra el Diseñador de dimensiones para la dimensión Customer. Para ello, haga doble clic en la dimensión **Customer** del nodo **Dimensiones** del Explorador de soluciones.  
  
2.  En el panel **Atributos** , observe los atributos Customer Key y Geography Key creados mediante el Asistente para cubos.  
  
3.  En la barra de herramientas de la pestaña **Estructura de dimensión** , asegúrese de que el icono Zoom para ver las tablas del panel **Vista del origen de datos** está establecido al 100 por cien.  
  
4.  Arrastre las columnas siguientes de la tabla **Customer** del panel **Vista del origen de datos** al panel **Atributos** :  
  
    -   **BirthDate**  
  
    -   **MaritalStatus**  
  
    -   **Sexo**  
  
    -   **EmailAddress**  
  
    -   **YearlyIncome**  
  
    -   **TotalChildren**  
  
    -   **NumberChildrenAtHome**  
  
    -   **EnglishEducation**  
  
    -   **EnglishOccupation**  
  
    -   **HouseOwnerFlag**  
  
    -   **NumberCarsOwned**  
  
    -   **Teléfono**  
  
    -   **DateFirstPurchase**  
  
    -   **CommuteDistance**  
  
5.  Arrastre las columnas siguientes de la tabla **Geography** del panel **Vista del origen de datos** al panel **Atributos** :  
  
    -   **Ciudad**  
  
    -   **StateProvinceName**  
  
    -   **SpanishCountryRegionName**  
  
    -   **PostalCode**  
  
6.  En el menú Archivo, haga clic en **Guardar todo**.  
  
## <a name="adding-attributes-to-the-product-dimension"></a>Agregar atributos a la dimensión Product  
  
#### <a name="to-add-attributes"></a>Para agregar atributos  
  
1.  Abra el Diseñador de dimensiones para la dimensión Product. Haga doble clic en la dimensión **Product** en el Explorador de soluciones.  
  
2.  En el panel **Atributos** , observe el atributo Product Key creado mediante el Asistente para cubos.  
  
3.  En la barra de herramientas de la pestaña **Estructura de dimensión** , asegúrese de que el icono Zoom para ver las tablas del panel **Vista del origen de datos** está establecido al 100 por cien.  
  
4.  Arrastre las columnas siguientes de la tabla **Product** del panel **Vista del origen de datos** al panel **Atributos** :  
  
    -   **StandardCost**  
  
    -   **Color**  
  
    -   **SafetyStockLevel**  
  
    -   **ReorderPoint**  
  
    -   **ListPrice**  
  
    -   **Tamaño**  
  
    -   **SizeRange**  
  
    -   **Peso**  
  
    -   **DaysToManufacture**  
  
    -   **ProductLine**  
  
    -   **DealerPrice**  
  
    -   **Clase**  
  
    -   **Estilo**  
  
    -   **ModelName**  
  
    -   **StartDate**  
  
    -   **EndDate**  
  
    -   **Estado**  
  
5.  En el menú Archivo, haga clic en **Guardar todo**.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Revisar las propiedades de cubo y dimensión](../analysis-services/lesson-2-4-reviewing-cube-and-dimension-properties.md)  
  
## <a name="see-also"></a>Vea también  
[Referencia de las propiedades de los atributos de dimensión](../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
  
