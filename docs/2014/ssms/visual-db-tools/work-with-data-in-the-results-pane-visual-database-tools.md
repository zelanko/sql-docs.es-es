---
title: Trabajar con datos en el panel Resultados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- queries [Visual Database Tools]
- result sets [SQL Server], queries
- Query Designer [SQL Server], Results pane
- results [SQL Server], query
- Visual Database Tools [SQL Server], queries
- queries [SQL Server], results
- Results pane
ms.assetid: 4f8a0080-91ef-4442-83ae-53be2f478c54
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d5f3dffc7661fc5843dcd220f27beb1117a85729
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63313772"
---
# <a name="work-with-data-in-the-results-pane-visual-database-tools"></a>Trabajar con datos en el panel Resultados (Visual Database Tools)
  Después de ejecutar una consulta o vista, los resultados se muestran en el panel Resultados. A continuación, puede trabajar con esos resultados. Por ejemplo, puede agregar y eliminar filas, especificar o modificar datos y navegar fácilmente entre conjuntos de resultados de gran tamaño.  
  
 La información siguiente puede ayudarle a evitar problemas y a trabajar eficazmente con sus conjuntos de resultados.  
  
## <a name="returning-the-results-set"></a>Devolver el conjunto de resultados  
 Puede devolver los resultados de una consulta o una vista y puede elegir entre abrir solo el panel de resultados o todos los paneles. En ambos casos, la consulta o la vista se abrirá en el Diseñador de consultas y vistas. La única diferencia es que en el primer caso se abrirá mostrando solo el panel Resultados y en el segundo se abrirá mostrando todas las ventanas que se hayan seleccionado en el cuadro de diálogo Opciones. El valor predeterminado es mostrar los cuatro paneles (Resultados, SQL, Diagrama y Criterios).  
  
 Para más información, consulte [Abrir consultas &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
 Para cambiar el diseño de la consulta o vista de modo que devuelva un conjunto de resultados diferente, o bien los registros en otro orden, consulte [Temas de procedimientos de diseño de consultas y vistas &#40;Visual Database Tools&#41;](design-queries-and-views-how-to-topics-visual-database-tools.md).  
  
 También puede elegir entre dos formas de devolver todo o parte del conjunto de resultados: detener la consulta durante su ejecución o elegir cuántos resultados deben devolverse antes de ejecutar la consulta.  
  
## <a name="navigating-in-the-results-pane"></a>Desplazarse por el panel Resultados  
 Puede navegar rápidamente por los registros utilizando la barra de navegación de la parte inferior del panel Resultados.  
  
 Hay botones para ir al primer y último registro, al registro anterior y siguiente, y para ir a un registro concreto.  
  
 Para ir a un registro concreto, escriba el número de la fila en el cuadro de texto de la barra de navegación y, a continuación, presione ENTRAR.  
  
 Para información sobre cómo usar los métodos abreviados de teclado en el Diseñador de consultas y vistas, consulte [Desplazarse por el Diseñador de consultas y vistas &#40;Visual Database Tools&#41;](navigate-in-the-query-and-view-designer-visual-database-tools.md).  
  
## <a name="committing-changes-to-the-database"></a>Confirmar cambios en la base de datos.  
 El panel Resultados utiliza el control de simultaneidad optimista para que la cuadrícula muestre una copia de los datos de la base de datos en lugar de una vista completamente activa. De este modo, los cambios solo se confirman en la base de datos después de salir de una fila. Esto permite que varios usuarios puedan trabajar al mismo tiempo en la base de datos. Si hay conflictos (por ejemplo si otro usuario cambia la misma fila y la confirma en la base de datos antes que usted) recibirá un mensaje en el que se le notificará la existencia del conflicto y se le ofrecerán soluciones.  
  
## <a name="undo-changes-using-esc"></a>Deshacer cambios mediante ESC  
 Solo puede deshacer un cambio si no se ha confirmado aún en la base de datos. Los datos no se confirmarán si no sale del registro, o si una vez fuera del registro recibe un mensaje de error que le indica que no se va a confirmar el cambio. Si no se ha realizado la confirmación, puede deshacer el cambio utilizando la tecla ESC.  
  
 Para deshacer todos los cambios de una fila, desplácese a una celda de la misma que no haya editado y presione la tecla ESC.  
  
 Para deshacer los cambios a una celda concreta que haya editado, desplácese hasta esa celda y presione la tecla ESC.  
  
## <a name="adding-or-deleting-data-in-the-database"></a>Agregar o eliminar datos de la base de datos  
 Para ver cómo funciona el diseño de la base de datos, puede que necesite agregar datos de ejemplo. Puede escribirlos directamente en el panel de resultados o copiarlos de otro programa, como bloque de notas o Excel, y pegarlo en el panel de resultados.  
  
 Además de copiar filas en el panel Resultados, puede agregar nuevos registros, modificar los existentes o eliminarlos. Para más información, consulte [Agregar nuevas filas en el panel Resultados &#40;Visual Database Tools&#41;](results-pane-visual-database-tools.md), [Eliminar filas en el panel Resultados &#40;Visual Database Tools&#41;](delete-rows-in-the-results-pane-visual-database-tools.md) y [Editar filas del panel Resultados &#40;Visual Database Tools&#41;](edit-rows-in-the-results-pane-visual-database-tools.md).  
  
## <a name="tips-for-working-with-null-values-and-empty-cells"></a>Sugerencias para trabajar con valores NULL y celdas vacías  
 Al hacer clic en una fila vacía para agregar un nuevo registro, el valor inicial de todas las columnas es *NULL*. Si la columna permite valores NULL, puede dejarla como está.  
  
 Si desea sustituir un valor no NULL por un valor NULL, escriba NULL con letras mayúsculas. El panel Resultados aplicará formato de cursiva a la palabra para indicar que se va a reconocer como un valor NULL en lugar de como una cadena.  
  
 Para especificar el tipo "NULL" de la cadena no lo escriba entre comillas. Siempre que ,por lo menos, una de las letras se escriba en minúscula, el valor se tratará como una cadena y no como valor nulo.  
  
 Los valores de las columnas con un tipo de datos binario tendrán valores NULL de manera predeterminada. Estos valores no se pueden cambiar en el panel Resultados.  
  
 Para escribir un espacio vacío en lugar de utilizar un valor NULL, elimine el texto existente y salga de la celda.  
  
## <a name="validating-data"></a>Validar los datos  
 El Diseñador de consultas y vistas puede validar algunos tipos de datos cotejándolos con las propiedades de columnas. Por ejemplo, si escribe "abc" en una columna con un tipo de datos float, recibirá un error y el cambio no se confirmará en la base de datos.  
  
 La manera más rápida de ver el tipo de datos de una columna en el panel Resultados es abrir el panel Diagrama y mantener el mouse sobre el nombre de la columna de la tabla u objeto con valores de tabla.  
  
> [!NOTE]  
>  La longitud máxima que puede mostrar el panel Resultados para un tipo de datos de texto es 2.147.483.647.  
  
## <a name="keeping-the-results-set-synchronized-with-the-query-definition"></a>Mantener el conjunto de resultados sincronizado con la definición de la consulta  
 Mientras se trabaja en los resultados de una consulta o vista, es posible que los registros del panel de resultados no estén sincronizados con la definición de las consultas. Por ejemplo, si se ejecutara una consulta para cuatro de las cinco columnas de una tabla y, a continuación, se utilizara el panel Diagrama para agregar la quinta columna a la definición de la consulta, los datos de esa quinta columna no se agregarán automáticamente al panel de resultados. Para hacer que el panel de resultados refleje la nueva definición, vuelva a ejecutar la consulta.  
  
 Si esto ocurre, aparecerá un icono de alerta y el texto "Consulta cambiada" en la esquina inferior derecha del panel de resultados, y el icono aparecerá repetido en la esquina superior izquierda del panel.  
  
## <a name="reconciling-changes-made-by-multiple-users"></a>Reconciliar los cambios realizados por varios usuarios  
 Mientras se trabaja en los resultados de una consulta o vista, es el posible que otro usuario que esté trabajando en la base de datos al mismo tiempo cambie los registros.  
  
 Si esto ocurre, recibirá un aviso en cuanto salga de la celda que entra en conflicto. A continuación, podrá elegir entre reemplazar el cambio del otro usuario, actualizar su panel de resultados con el cambio del otro usuario o seguir editando el panel de resultados sin reconciliar las diferencias. Si decide no reconciliar las diferencias, los cambios no se confirmarán en la base de datos.  
  
## <a name="limitations-in-the-results-pane"></a>Limitaciones del panel Resultados  
  
### <a name="what-can-not-be-updated"></a>Lo que no puede actualizarse  
 Estas sugerencias pueden ayudarle a trabajar correctamente con datos en el panel Resultados.  
  
-   Las consultas que incluyen columnas de más de una tabla o vista no pueden actualizarse.  
  
-   Las vistas solo pueden actualizarse si las restricciones de base de datos lo permiten.  
  
-   Los resultados devueltos mediante un procedimiento almacenado no pueden actualizarse.  
  
-   Las consultas o vistas que utilizan las cláusulas GROUP BY, DISTINCT o TO XML no se pueden actualizar.  
  
-   Los resultados devueltos mediante funciones con valores de tabla solo pueden actualizarse en algunos casos.  
  
-   Datos de columnas que son el resultado de una expresión de la consulta.  
  
-   Datos que el proveedor no ha traducido correctamente.  
  
### <a name="what-can-not-be-represented-fully"></a>Lo que no puede representarse totalmente  
 Lo que se devuelve al panel Resultados desde la base de datos está controlado en gran medida por el proveedor del origen de datos que se está utilizando. El panel Resultados no siempre puede traducir los datos de todos los sistemas de administración de bases de datos. A continuación, se enumeran algunos de estos casos.  
  
-   Los tipos de datos binarios no suelen resultar útiles para los usuarios que trabajan en el panel Resultados, ya que pueden tardar mucho tiempo en descargarse. Por tanto, se representan mediante * \<datos binarios>* o *null*.  
  
-   La precisión y la escala no siempre pueden conservarse. Por ejemplo, el panel Resultados admite una precisión de 27. Si los datos son de un tipo de datos con una precisión mayor, los datos se pueden truncar o pueden estar representados por * \<no se pueden leer los datos>*.  
  
## <a name="see-also"></a>Consulte también  
 [Realizar operaciones básicas con consultas &#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)   
 [Especificar criterios de búsqueda (Visual Database Tools)](specify-search-criteria-visual-database-tools.md)  
  
  
