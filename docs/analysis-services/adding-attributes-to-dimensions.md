---
title: "Agregar atributos a dimensiones | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 80551dad-97ac-40d0-90af-b810780321ce
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Agregar atributos a dimensiones
Ahora que ha definido las dimensiones, puede rellenarlas con atributos que representan cada elemento de datos de la dimensión. Los atributos suelen estar basados en campos de una vista del origen de datos. Al agregar atributos a una dimensión, puede incluir campos de cualquier tabla de la vista del origen de datos.  
  
En esta tarea, usará el Diseñador de dimensiones para agregar atributos a las dimensiones Customer y Product. La dimensión Customer incluirá atributos basados en campos de las tablas Customer y Geography.  
  
## Agregar atributos a la dimensión Customer  
  
#### Para agregar atributos  
  
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
  
## Agregar atributos a la dimensión Product  
  
#### Para agregar atributos  
  
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
  
## Siguiente tarea de la lección  
[Revisar las propiedades de cubo y dimensión](../analysis-services/reviewing-cube-and-dimension-properties.md)  
  
## Vea también  
[Referencia de las propiedades de los atributos de dimensión](../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
  
