---
title: Crear una tabla calculada | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f920d7ef7ae8a8fb5016e4bb4833b3637b325f8a
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-a-calculated-table"></a>Crear una tabla calculada 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Una *tabla calculada* es un objeto calculado que se basa en una expresión o consulta DAX derivada del resto de tablas del mismo modelo (o de una parte).  
  
 Un problema habitual de diseño que las tablas calculadas pueden resolver es exponer una dimensión realizadora de roles en un contexto específico para que se pueda exponer como una estructura de consulta en aplicaciones cliente.  Como probablemente recuerde, una dimensión realizadora de roles es simplemente una tabla expuesta en varios contextos. Un ejemplo clásico es la tabla Date, manifestada como OrderDate, ShipDate o DueDate en función de la relación de clave externa. Al crear una columna calculada explícitamente para ShipDate, obtendrá una tabla independiente que está disponible para consultas, tan operativa como cualquier otra tabla.  
  
 Un segundo uso de las tablas calculadas incluye la configuración de un conjunto de filas filtrado o un subconjunto o superconjunto de columnas a partir de otras tablas existentes. Esto permite mantener intacta la tabla original a la vez que se crean variaciones de dicha tabla para admitir escenarios concretos.  
  
 Para aprovechar al máximo el uso de las tablas calculadas, debe tener conocimientos básicos de DAX. Cuando se trabaja con expresiones para la tabla, puede ser útil saber que una tabla calculada contiene una sola partición con un objeto DAXSource, donde la expresión es una expresión DAX.  
Hay un valor CalculatedTableColumn para cada columna que devuelve la expresión, donde SourceColumn es el nombre de la columna devuelta (similar a los objetos DataColumn de las tablas no calculadas).  
  
## <a name="how-to-create-a-calculated-table"></a>Cómo crear una tabla calculada  
  
1.  En primer lugar, compruebe que el modelo tabular tenga un nivel de compatibilidad de 1200 o superior. Puede comprobar la propiedad **ivel de compatibilidad** del modelo en SSDT.  
  
2.  Cambie a la vista de datos. No se puede crear una tabla calculada en la vista de diagrama.  
  
3.  Seleccione **Tabla** > **Nueva tabla calculada**.  
  
4.  Escriba o pegue una expresión DAX (más abajo encontrará unas cuantas ideas).  
  
5.  Asígnele un nombre a la tabla.  
  
6.  Cree relaciones con otras tablas del modelo. Vea [crear una relación entre dos tablas](../../analysis-services/tabular-models/create-a-relationship-between-two-tables-ssas-tabular.md) si necesita ayuda con este paso.  
  
7.  Haga referencia a la tabla en los cálculos o las expresiones del modelo o use **Analizar en Excel** para realizar una exploración de datos ad hoc.  
  
### <a name="replicate-a-role-playing-dimension"></a>Replicar una dimensión realizadora de roles  
 En la barra de fórmulas, escriba una fórmula DAX que obtenga una copia de otra tabla. Una vez que se rellene la tabla calculada, asígnele un nombre descriptivo y configure una relación que use la clave externa específica del rol. Por ejemplo, en la base de datos de Adventure Works, puede crear una tabla calculada para la fecha de vencimiento y usar DueDateKey como base de una relación con la tabla de hechos.  
  
```  
=DimDate  
```  
  
### <a name="summarized-or-filtered-dataset"></a>Conjunto de datos resumido o filtrado  
 En la barra de fórmulas, escriba una expresión DAX que filtre, resuma o manipule de otro modo un conjunto de datos para que contenga las filas que quiera. En este ejemplo se realiza una agrupación por ventas, color y divisa.  
  
```  
=SUMMARIZECOLUMNS(DimProduct[Color]  
, DimCurrency[CurrencyName]   
, "Sales" , SUM(FactInternetSales[SalesAmount])  
)  
```  
  
### <a name="superset-using-columns-from-multiple-tables"></a>Superconjunto con columnas de varias tablas  
 En la barra de fórmulas, escriba una expresión DAX que combine columnas de varias tablas. En este caso, la salida de la consulta muestra la categoría de productos de cada divisa.  
  
```  
=CROSSJOIN(DimProductCategory, DimCurrency)  
```  
  
## <a name="see-also"></a>Vea también  
 [Nivel de compatibilidad](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Expresiones de análisis de datos &#40;DAX&#41; en Analysis Services](http://msdn.microsoft.com/library/abb336c9-3346-4cab-b91b-90f93f4575e5)   
 [Descripción de DAX en modelos tabulares](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)  
  
  
