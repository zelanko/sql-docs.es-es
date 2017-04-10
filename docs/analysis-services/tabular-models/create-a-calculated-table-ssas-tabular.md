---
title: "Crear una tabla calculada (SSAS tabular) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d7ff98a-82a9-4333-a7d3-7a95a6f2caf7
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 10
---
# Crear una tabla calculada (SSAS tabular)
  Una *tabla calculada* es un objeto calculado que se basa en una expresión o consulta DAX derivada del resto de tablas del mismo modelo (o de una parte).  
  
 Un problema habitual de diseño que las tablas calculadas pueden resolver es exponer una dimensión realizadora de roles en un contexto específico para que se pueda exponer como una estructura de consulta en aplicaciones cliente.  Como probablemente recuerde, una dimensión realizadora de roles es simplemente una tabla expuesta en varios contextos. Un ejemplo clásico es la tabla Date, manifestada como OrderDate, ShipDate o DueDate en función de la relación de clave externa. Al crear una columna calculada explícitamente para ShipDate, obtendrá una tabla independiente que está disponible para consultas, tan operativa como cualquier otra tabla.  
  
 Un segundo uso de las tablas calculadas incluye la configuración de un conjunto de filas filtrado o un subconjunto o superconjunto de columnas a partir de otras tablas existentes. Esto permite mantener intacta la tabla original a la vez que se crean variaciones de dicha tabla para admitir escenarios concretos.  
  
 Para aprovechar al máximo el uso de las tablas calculadas, debe tener conocimientos básicos de DAX. Cuando se trabaja con expresiones para la tabla, puede ser útil saber que una tabla calculada contiene una sola partición con un objeto DAXSource, donde la expresión es una expresión DAX.  
Hay un valor CalculatedTableColumn para cada columna que devuelve la expresión, donde SourceColumn es el nombre de la columna devuelta (similar a los objetos DataColumn de las tablas no calculadas).  
  
## Cómo crear una tabla calculada  
  
1.  En primer lugar, compruebe que el modelo tabular tenga un nivel de compatibilidad 1200. Puede comprobar la propiedad **ivel de compatibilidad** del modelo en SSDT.  
  
2.  Cambie a la vista de datos. No se puede crear una tabla calculada en la vista de diagrama.  
  
3.  Seleccione **Tabla** > **Nueva tabla calculada**.  
  
4.  Escriba o pegue una expresión DAX (más abajo encontrará unas cuantas ideas).  
  
5.  Asígnele un nombre a la tabla.  
  
6.  Cree relaciones con otras tablas del modelo. Vea [Crear una relación entre dos tablas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md) si necesita ayuda con este paso.  
  
7.  Haga referencia a la tabla en los cálculos o las expresiones del modelo o use **Analizar en Excel** para realizar una exploración de datos ad hoc.  
  
### Replicar una dimensión realizadora de roles  
 En la barra de fórmulas, escriba una fórmula DAX que obtenga una copia de otra tabla. Una vez que se rellene la tabla calculada, asígnele un nombre descriptivo y configure una relación que use la clave externa específica del rol. Por ejemplo, en la base de datos de Adventure Works, puede crear una tabla calculada para la fecha de vencimiento y usar DueDateKey como base de una relación con la tabla de hechos.  
  
```  
=DimDate  
```  
  
### Conjunto de datos resumido o filtrado  
 En la barra de fórmulas, escriba una expresión DAX que filtre, resuma o manipule de otro modo un conjunto de datos para que contenga las filas que quiera. En este ejemplo se realiza una agrupación por ventas, color y divisa.  
  
```  
=SUMMARIZECOLUMNS(DimProduct[Color]  
, DimCurrency[CurrencyName]   
, "Sales" , SUM(FactInternetSales[SalesAmount])  
)  
```  
  
### Superconjunto con columnas de varias tablas  
 En la barra de fórmulas, escriba una expresión DAX que combine columnas de varias tablas. En este caso, la salida de la consulta muestra la categoría de productos de cada divisa.  
  
```  
=CROSSJOIN(DimProductCategory, DimCurrency)  
```  
  
## Vea también  
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Data Analysis Expressions &#40;DAX&#41; in Analysis Services (Expresiones de análisis de datos (DAX) en Analysis Services)](../Topic/Data%20Analysis%20Expressions%20\(DAX\)%20in%20Analysis%20Services.md)   
 [Descripción de DAX en modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)  
  
  