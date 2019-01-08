---
title: Calcula las columnas de modelos tabulares de Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 087c30045fdee1e769471cb12188cf31b524c618
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072402"
---
# <a name="calculated-columns"></a>Columnas calculadas
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Las columnas calculadas, en los modelos tabulares, podrá agregar nuevos datos al modelo. En lugar de pegar o importar los valores en la columna, cree una fórmula DAX que define los valores de nivel de fila de la columna. A continuación, la columna calculada se puede utilizar en un informe, una tabla dinámica o un gráfico dinámico como cualquier otra columna.  
 
  
  
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
  
##  <a name="bkmk_naming"></a> Naming a calculated column  
 De forma predeterminada, las columnas calculadas nuevas se agregan a la derecha de las demás columnas de la tabla y reciben automáticamente el nombre predeterminado **CalculatedColumn1**, **CalculatedColumn2**, etc. Para crear una nueva columna entre dos columnas existentes, también puede hacer clic con el botón secundario en una columna y, a continuación, hacer clic en Insertar columna. Puede reorganizar columnas de la misma tabla haciendo clic y arrastrando, así como cambiar su nombre una vez creadas; sin embargo, debe tener en cuenta las restricciones siguientes respecto a los cambios en columnas calculadas:  
  
-   Cada nombre de columna deben ser único en una tabla.  
  
-   Evite nombres que ya ha usado para las medidas dentro del mismo modelo. Aunque es posible que una medida y una columna calculada tengan el mismo nombre, si los nombres no son únicos puede obtener errores de cálculo. Para no invocar una medida accidentalmente, al hacer referencia a una columna use siempre una referencia de columna completa.  
  
-   Al cambiar el nombre de una columna calculada, se deben actualizar manualmente las fórmulas que se basan en dicha columna. A menos que esté en modo de actualización manual, la actualización de los resultados de las fórmulas tiene lugar automáticamente. Sin embargo, esta operación podría tardar algún tiempo.  
  
-   Algunos caracteres no se pueden usar en los nombres de columnas. Para más información, consulte los requisitos de nomenclatura en [DAX Syntax Reference](http://msdn.microsoft.com/098630f4-7d1d-467e-976c-99b2279430d5)(Referencia de sintaxis de DAX).  
  
##  <a name="bkmk_perf"></a> Performance of calculated columns  
 La fórmula para una columna calculada puede consumir más recursos que la fórmula para una medida. Uno de los motivos para ello es que el resultado de una columna calculada siempre se calcula para cada fila de una tabla, mientras que una medida solo se calcula para las celdas definidas por el filtro utilizado en un informe, una tabla dinámica o un gráfico dinámico. Por ejemplo, una tabla con un millón de filas siempre tendrá una columna calculada con un millón de resultados y un efecto correspondiente en el rendimiento. Sin embargo, una tabla dinámica generalmente filtra los datos aplicando encabezados de columnas y de filas; por consiguiente, una medida solo se calcula para el subconjunto de datos en cada celda de la tabla dinámica.  
  
 Una fórmula depende de los objetos a los que se hacen referencia en la fórmula, como otras columnas o expresiones que evalúan valores. Por ejemplo, una columna calculada que está basada en otra columna o un cálculo que contiene una expresión con una referencia de columna no se puede evaluar hasta que se evalúe la otra columna. De forma predeterminada, la actualización automática está habilitada en los libros; por consiguiente, tales dependencias pueden afectar a rendimiento mientras los valores y las fórmulas se actualizan.  
  
 Para evitar tener problemas con el rendimiento al crear columnas calculadas, siga estas directrices:  
  
-   En lugar de crear una única fórmula que contenga muchas dependencias complejas, cree las fórmulas en pasos y guarde los resultados en las columnas, de modo que pueda validarlos y evaluar el rendimiento.  
  
-   Con frecuencia, la modificación de datos requiere que se actualicen las columnas calculadas. Puede evitarlo estableciendo el modo de recálculo en manual; no obstante, si cualquiera de los valores de la columna calculada es incorrecto, aparecerá deshabilitada hasta que se actualicen y recalculen los datos.  
  
-   Si cambia o elimina las relaciones entre las tablas, las fórmulas que usan las columnas de esas tablas dejarán de ser válidas.  
  
-   Si crea una fórmula que contenga una referencia circular o que se haga referencia a sí misma, se producirá un error.  
  
##  <a name="bkmk_rel_tasks"></a> Related tasks  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Crear una columna calculada](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)|En las tareas de este tema se describe cómo agregar una nueva columna calculada a una tabla.|  
  
## <a name="see-also"></a>Vea también  
 [Tablas y columnas](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Cálculos](../../analysis-services/tabular-models/calculations-ssas-tabular.md)  
  
  
