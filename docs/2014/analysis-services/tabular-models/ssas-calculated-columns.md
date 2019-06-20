---
title: Calcula las columnas (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: e1011278-556d-4984-b01d-a37f8a33b304
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0ad2e89a8862c4b51856d70ddb1dfd3b1e1fdb17
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66066583"
---
# <a name="calculated-columns-ssas-tabular"></a>Columnas calculadas (SSAS tabular)
  En los modelos tabulares, las columnas calculadas le permiten agregar nuevos datos al modelo. En lugar de pegar o importar los valores en la columna, cree una fórmula DAX que define los valores de nivel de fila de la columna. A continuación, la columna calculada se puede utilizar en un informe, una tabla dinámica o un gráfico dinámico como cualquier otra columna.  
  
> [!NOTE]  
>  Las columnas calculadas no se admiten en los modelos tabulares en el modo DirectQuery. Para más información, vea [Modo DirectQuery &#40;SSAS tabular&#41;](directquery-mode-ssas-tabular.md).  
  
 Secciones de este tema:  
  
-   [Ventajas](#bkmk_understanding)  
  
-   [Cambiar el nombre de una columna calculada](#bkmk_naming)  
  
-   [Rendimiento de las columnas calculadas](#bkmk_perf)  
  
-   [Tareas relacionadas](#bkmk_rel_tasks)  
  
##  <a name="bkmk_understanding"></a> Ventajas  
 Las fórmulas en las columnas calculadas son muy similares a las fórmulas en Excel. A diferencia de Excel, sin embargo, no se pueden crear fórmulas diferentes para las distintas filas de una tabla; la fórmula de DAX se aplica automáticamente a toda la columna.  
  
 Cuando una columna contiene una fórmula, el valor se calcula para cada fila. Los resultados se calculan para la columna cuando se escribe una fórmula válida. A continuación, los valores de columna se actualizan según convenga, por ejemplo cuando los datos subyacentes se actualizan.  
  
 Puede crear columnas calculadas que están basadas en las medidas y en otras columnas calculadas. Por ejemplo, se podría crear una columna calculada para extraer un número de una cadena de texto y, a continuación, usar ese número en otra columna calculada.  
  
 Una columna calculada está basada en datos ya incluidos en una tabla existente, o que se crean mediante una fórmula de DAX. Por ejemplo, podría decidir concatenar los valores, realizar la suma, extraer las subcadenas o comparar los valores de otros campos. Para agregar una columna calculada, debe haber al menos una tabla en el modelo.  
  
 En este ejemplo se muestra una fórmula simple en una columna calculada:  
  
```  
=EOMONTH([StartDate],0])  
  
```  
  
 Esta fórmula extrae el mes de la columna StartDate. A continuación, calcula el valor del fin de mes de cada fila de la tabla. El segundo parámetro especifica el número de meses antes o después del mes en StartDate; en este caso, 0 significa el mismo mes. Por ejemplo, si el valor de la columna StartDate es 6/1/2001, el valor de la columna calculada será 6/30/2001.  
  
##  <a name="bkmk_naming"></a> Cambiar el nombre de una columna calculada  
 De forma predeterminada, las columnas calculadas nuevas se agregan a la derecha de las demás columnas de la tabla y reciben automáticamente el nombre predeterminado **CalculatedColumn1**, **CalculatedColumn2**, etc. Para crear una nueva columna entre dos columnas existentes, también puede hacer clic con el botón secundario en una columna y, a continuación, hacer clic en Insertar columna. Puede reorganizar columnas de la misma tabla haciendo clic y arrastrando, así como cambiar su nombre una vez creadas; sin embargo, debe tener en cuenta las restricciones siguientes respecto a los cambios en columnas calculadas:  
  
-   Cada nombre de columna deben ser único en una tabla.  
  
-   Evite nombres que ya ha usado para las medidas dentro del mismo modelo. Aunque es posible que una medida y una columna calculada tengan el mismo nombre, si los nombres no son únicos puede obtener errores de cálculo. Para no invocar una medida accidentalmente, al hacer referencia a una columna use siempre una referencia de columna completa.  
  
-   Al cambiar el nombre de una columna calculada, se deben actualizar manualmente las fórmulas que se basan en dicha columna. A menos que esté en modo de actualización manual, la actualización de los resultados de las fórmulas tiene lugar automáticamente. Sin embargo, esta operación podría tardar algún tiempo.  
  
-   Algunos caracteres no se pueden usar en los nombres de columnas. Para obtener más información, vea los requisitos de denominación en [DAX Syntax Specification for PowerPivot](https://msdn.microsoft.com/library/ee634217(v=sql.120).aspx).  
  
##  <a name="bkmk_perf"></a> Rendimiento de las columnas calculadas  
 La fórmula para una columna calculada puede consumir más recursos que la fórmula para una medida. Uno de los motivos para ello es que el resultado de una columna calculada siempre se calcula para cada fila de una tabla, mientras que una medida solo se calcula para las celdas definidas por el filtro utilizado en un informe, una tabla dinámica o un gráfico dinámico. Por ejemplo, una tabla con un millón de filas siempre tendrá una columna calculada con un millón de resultados y un efecto correspondiente en el rendimiento. Sin embargo, una tabla dinámica generalmente filtra los datos aplicando encabezados de columnas y de filas; por consiguiente, una medida solo se calcula para el subconjunto de datos en cada celda de la tabla dinámica.  
  
 Una fórmula depende de los objetos a los que se hacen referencia en la fórmula, como otras columnas o expresiones que evalúan valores. Por ejemplo, una columna calculada que está basada en otra columna o un cálculo que contiene una expresión con una referencia de columna no se puede evaluar hasta que se evalúe la otra columna. De forma predeterminada, la actualización automática está habilitada en los libros; por consiguiente, tales dependencias pueden afectar a rendimiento mientras los valores y las fórmulas se actualizan.  
  
 Para evitar tener problemas con el rendimiento al crear columnas calculadas, siga estas directrices:  
  
-   En lugar de crear una única fórmula que contenga muchas dependencias complejas, cree las fórmulas en pasos y guarde los resultados en las columnas, de modo que pueda validarlos y evaluar el rendimiento.  
  
-   Con frecuencia, la modificación de datos requiere que se actualicen las columnas calculadas. Puede evitarlo estableciendo el modo de recálculo en manual; no obstante, si cualquiera de los valores de la columna calculada es incorrecto, aparecerá deshabilitada hasta que se actualicen y recalculen los datos.  
  
-   Si cambia o elimina las relaciones entre las tablas, las fórmulas que usan las columnas de esas tablas dejarán de ser válidas.  
  
-   Si crea una fórmula que contenga una referencia circular o que se haga referencia a sí misma, se producirá un error.  
  
##  <a name="bkmk_rel_tasks"></a> Tareas relacionadas  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Crear una columna calculada &#40;SSAS tabular&#41;](ssas-calculated-columns-create-a-calculated-column.md)|En las tareas de este tema se describe cómo agregar una nueva columna calculada a una tabla.|  
  
## <a name="see-also"></a>Vea también  
 [Definir tablas y columnas &#40;SSAS tabular&#41;](tables-and-columns-ssas-tabular.md)   
 [Medidas &#40;SSAS tabular&#41;](measures-ssas-tabular.md)   
 [Cálculos &#40;SSAS tabular&#41;](calculations-ssas-tabular.md)  
  
  
