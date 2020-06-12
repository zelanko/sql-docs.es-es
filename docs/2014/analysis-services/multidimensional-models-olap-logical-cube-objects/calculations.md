---
title: Cálculos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- calculations [Analysis Services]
- OLAP objects [Analysis Services], calculations
- MDX [Analysis Services], calculations
- calculations [Analysis Services], about calculations
- cubes [Analysis Services], calculations
ms.assetid: 6be84916-fd05-4efc-ab98-6adbbad80154
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4457a5fa434be3865edf770f7ca69a676c051893
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545347"
---
# <a name="calculations"></a>Cálculos
  Un cálculo es una expresión o un script MDX (expresiones multidimensionales) que se utiliza para definir un miembro calculado, un conjunto con nombre o una asignación de ámbito en un cubo de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Los cálculos permiten agregar objetos definidos no por los datos del cubo, sino por expresiones que pueden hacer referencia a otras partes del cubo, a otros cubos o incluso a información que se encuentra fuera de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Los cálculos permiten ampliar las capacidades de un cubo, al aumentar la flexibilidad y la eficacia de las aplicaciones de Business Intelligence. Para obtener más información acerca de los cálculos de scripting, vea [Introducción al scripting de MDX en Microsoft SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=81892). Para obtener más información acerca de los problemas de rendimiento relacionados con las consultas y los cálculos de MDX, vea la [Guía de rendimiento de SQL Server 2005 Analysis Services](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide).  
  
## <a name="calculated-members"></a>Miembros calculados  
 Un miembro calculado es un miembro cuyo valor se calcula en tiempo de ejecución mediante una expresión MDX (Expresiones multidimensionales) que se especifica al definir el miembro calculado. Los miembros calculados están disponibles para las aplicaciones de Business Intelligence del mismo modo que los demás miembros. Los miembros calculados no aumentan el tamaño del cubo porque en el mismo solamente se almacenan las definiciones; los valores se calculan en la memoria cuando son necesarios para responder a una consulta.  
  
 Los miembros calculados se pueden definir para cualquier dimensión, incluida la dimensión de medidas. Los miembros calculados creados en la dimensión de medidas se denominan medidas calculadas.  
  
 Aunque los miembros calculados normalmente se basan en los datos que ya existen en un cubo, puede crear expresiones complejas si combina datos con operadores aritméticos, números y funciones. También puede usar funciones MDX, como LookupCube, para tener acceso a los datos de otros cubos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluye bibliotecas normalizadas de funciones de Visual Studio y permite usar procedimientos almacenados para recuperar datos de otros orígenes distintos a la base de datos actual de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Para obtener más información acerca de los procedimientos almacenados, vea [definir procedimientos almacenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md).  
  
 Por ejemplo, suponga que los ejecutivos de una naviera desean determinar qué tipos de carga son más rentables basándose en el beneficio por unidad de volumen. Utilizan un cubo denominado Shipments que contiene las dimensiones Cargo, Fleet y Time y las medidas Price_to_Ship, Cost_to_Ship y Volume_in_Cubic_Meters; sin embargo, el cubo no contiene ninguna medida para la rentabilidad. En el cubo, se puede crear un miembro calculado como medida que se denomine Profit_per_Cubic_Meter mediante la combinación de las medidas existentes en la siguiente expresión:  
  
```  
([Measures].[Price_to_Ship] - [Measures].[Cost_to_Ship]) /  
[Measures].[Volume_in_Cubic_Meters]  
```  
  
 Una vez creado el miembro calculado, Profit_per_Cubic_Meter aparecerá junto con otras medidas la siguiente vez que se examine el cubo Shipments.  
  
 Para crear miembros calculados, use la pestaña **Calculation**s del diseñador de cubos. Para obtener más información, vea [crear miembros calculados](../multidimensional-models/create-calculated-members.md) .  
  
## <a name="named-sets"></a>Conjuntos con nombre  
 Un conjunto con nombre es una expresión de instrucción MDX CREATE SET que devuelve un conjunto. La expresión MDX se guarda como parte de la definición de un cubo en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Un conjunto con nombre se crea para reutilizarse en consultas MDX (Expresiones Multidimensionales). Un conjunto con nombre permite a los usuarios corporativos simplificar las consultas y usar un nombre de conjunto en lugar de una expresión de conjunto para expresiones de conjunto complejas utilizadas con frecuencia. **Tema relacionado:** [crear conjuntos con nombre](../multidimensional-models/create-named-sets.md)  
  
## <a name="script-commands"></a>Comandos de script  
 Un comando de script es un script MDX, incluido como parte de la definición del cubo. Los comandos de script permiten realizar prácticamente cualquier acción admitida por MDX en un cubo, como asignar un ámbito a un cálculo que solamente se aplique a parte del cubo. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los scripts MDX se pueden aplicar a todo el cubo o a secciones específicas del cubo, en puntos específicos a lo largo de la ejecución del script. El comando de script predeterminado, que es la instrucción CALCULATE, rellena las celdas del cubo con datos agregados según el ámbito predeterminado.  
  
 El ámbito predeterminado es todo el cubo, pero puede definir un ámbito más restringido, denominado subcubo, y aplicar un script MDX solamente a dicho espacio de cubo. La instrucción SCOPE define el ámbito de todas las instrucciones y expresiones MDX posteriores en el script de cálculo hasta que finaliza o se vuelve a definir el ámbito. La instrucción THIS se utiliza para aplicar una expresión MDX al ámbito actual.  Puede utilizar la instrucción BACK_COLOR para especificar el color de fondo de celda de las celdas del ámbito actual, para ayudarle durante la depuración.   
  
 Por ejemplo, puede utilizar un comando de script para asignar cuotas de venta a los empleados a lo largo del tiempo y el territorio de ventas según los valores ponderados de las ventas de un período de tiempo anterior.  
  
## <a name="see-also"></a>Consulte también  
 [Cálculos en modelos multidimensionales](../multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
