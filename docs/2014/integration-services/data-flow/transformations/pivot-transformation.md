---
title: Transformación dinámica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.pivottrans.f1
helpviewer_keywords:
- Pivot transformation
- normalized data [Integration Services]
- PivotUsage property
- datasets [Integration Services], normalized data
- less normalized data set [Integration Services]
ms.assetid: 55f5db6e-6777-435f-8a06-b68c129f8437
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4bf9e58296b70f29e3e328782b463ecbbf7f6aab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770351"
---
# <a name="pivot-transformation"></a>Dinámica, transformación
  La transformación dinámica transforma un conjunto de datos normalizado en una versión menos normalizada pero más compacta dinamizando los datos de entrada en un valor de columna. Por ejemplo, un conjunto de datos **Orders** normalizado que enumera el nombre del cliente, el producto y la cantidad comprada normalmente tiene varias filas para cualquier cliente que compró varios productos, donde cada fila para ese cliente muestra los detalles de pedido de un producto diferente. Al dinamizar el conjunto de datos en la columna de producto, la transformación dinámica puede obtener un conjunto de datos con una sola fila por cliente. Esa única fila enumera todas las compras realizadas por el cliente, con los nombres de los productos representados como nombres de columnas, y la cantidad indicada como un valor en la columna de producto. Dado que no todos los clientes compran todos los productos, muchas columnas pueden contener valores NULL.  
  
 Cuando se dinamiza un conjunto de datos, las columnas de entrada ejecutan diferentes roles en el proceso de dinamización. Una columna puede participar de las siguientes maneras:  
  
-   La columna se pasa sin cambios a la salida. Dado que varias filas de entrada pueden obtener una sola fila de salida, la transformación copia solamente el primer valor de entrada para la columna.  
  
-   La columna funciona como la clave o parte de la clave que identifica un conjunto de registros.  
  
-   La columna define la dinamización. Los valores de esta columna se asocian con columnas en el conjunto de datos dinamizado.  
  
-   La columna contiene valores que se colocan en las columnas creadas por la dinamización.  
  
 Esta transformación tiene una entrada, una salida normal y una salida de error.  
  
## <a name="sort-and-duplicate-rows"></a>Ordenar y duplicar filas  
 Para dinamizar los datos de un modo eficaz, lo que significa crear la menor cantidad posible de registros en el conjunto de datos de salida, los datos de entrada se deben ordenar en la columna de dinamización. Si los datos no se ordenan, la transformación dinámica puede generar varios registros para cada valor en la clave fija, que es la columna que define la pertenencia a un conjunto. Por ejemplo, si un conjunto de datos se dinamiza en una columna **Name** pero los nombres no se ordenan, el conjunto de datos de salida puede tener más de una fila para cada cliente, porque se produce una dinamización cada vez que cambia el valor de **Name** .  
  
 Los datos de entrada pueden contener filas duplicadas, que darán lugar a que no funcione la transformación Dinamización. "Filas duplicadas" significa filas que tienen los mismos valores en las columnas de clave fija y las columnas dinámicas. Para evitar este error, puede configurar la transformación para que redirija las filas que causan el error hacia una salida de error, o bien agregar previamente valores para garantizar que no haya filas duplicadas.  
  
##  <a name="options"></a> Opciones del cuadro de diálogo Dinamización  
 Configure la operación de dinamizar, para lo cual se configuran las opciones en el cuadro de diálogo **Dinamización** . Para abrir el cuadro de diálogo **Dinamización** , agregue la transformación dinámica al paquete en [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], haga clic con el botón derecho en el componente y, después, haga clic en **Editar**.  
  
 En la lista siguiente, se describen las opciones en el cuadro de diálogo **Dinamización** .  
  
 **Clave dinámica**  
 Especifica la columna que se va a utilizar para los valores de toda la fila superior (fila de encabezado) de la tabla.  
  
 **Clave fija**  
 Especifica la columna que se va a usar para los valores en la columna izquierda de la tabla. La fecha de entrada se deben ordenar en esta columna.  
  
 **Valor dinámico**  
 Especifica la columna que se va a usar para los valores de la tabla, a excepción de los valores en la fila de encabezado y en la columna izquierda.  
  
 **Omitir valores de clave dinámica que no tengan coincidencias y notificarlos tras la ejecución de flujo de datos**  
 Seleccione esta opción para configurar la transformación dinámica con el fin de omitir las filas que contengan valores no reconocidos en la columna **Clave dinámica** y generar todos los valores de clave dinámica en un mensaje de registro cuando se ejecute el paquete.  
  
 También puede configurar la transformación para generar los valores si establece la propiedad personalizada `PassThroughUnmatchedPivotKeys` en `True`.  
  
 **Generar columnas de salida dinámicas a partir de valores**  
 Escriba los valores de clave dinámica en este cuadro para permitir la transformación dinámica con el fin de crear columnas de salida para cada valor. Puede especificar los valores antes de ejecutar el paquete o hacer lo siguiente.  
  
1.  Seleccione la opción **Omitir los valores de clave dinámica no coincidentes y registrarlos después de la ejecución del flujo de datos** y, después, haga clic en **Aceptar** en el cuadro de diálogo **Dinamización** para guardar los cambios en la transformación dinámica.  
  
2.  Ejecute el paquete.  
  
3.  Cuando el paquete se ejecute correctamente, haga clic en la pestaña **Progreso** y busque el mensaje del registro de información de la transformación dinámica que contiene los valores de clave dinámica.  
  
4.  Haga clic con el botón derecho en el mensaje y, después, haga clic en **Copiar texto del mensaje**.  
  
5.  Haga clic en **Detener depuración** en el menú **Depurar** para ir al modo de diseño.  
  
6.  Haga clic con el botón derecho en Transformación dinámica y, después, haga clic en **Editar**.  
  
7.  Desactive la opción **Omitir los valores de clave dinámica no coincidentes y registrarlos después de la ejecución del flujo de datos** y pegue los valores de clave dinámica en el cuadro **Generar columnas de salida dinámicas a partir de valores** con el formato siguiente.  
  
     [valor1],[valor2],[valor3]  
  
 **Generar columnas ahora**  
 Haga clic para crear una columna de salida por cada valor de clave dinámica que aparece en el cuadro **Generar columnas de salida dinámicas a partir de valores** .  
  
 Las columnas de salida aparecen en el cuadro **Columnas de salida dinámicas existentes** .  
  
 **Columnas de salida dinámicas existentes**  
 Muestra las columnas de salida para los valores de clave dinámica  
  
 En la tabla siguiente se muestra un conjunto de datos antes de dinamizar los datos en la columna **Year** .  
  
|Year|Nombre del producto|Total|  
|----------|------------------|-----------|  
|2004|HL Mountain Tire|1504884.15|  
|2003|Road Tire Tube|35920.50|  
|2004|Water Bottle - 30 oz.|2805.00|  
|2002|Touring tire|62364.225|  
  
 La tabla siguiente muestra un conjunto de datos después de que los datos se hayan dinamizado en la columna **Year** .  
  
||2002|2003|2004|  
|-|----------|----------|----------|  
|HL Mountain Tire|141164.10|446297.775|1504884.15|  
|Road Tire Tube|3592.05|35920.50|89801.25|  
|Water Bottle - 30 oz.|*NULL*|*NULL*|2805.00|  
|Touring tire|62364.225|375051.60|1041810.00|  
  
 Para dinamizar los datos de la columna **Year** , tal como se muestra más arriba, se establecen las opciones siguientes en el cuadro de diálogo **Dinamización** .  
  
-   El año está seleccionado en el cuadro de lista **Clave dinámica** .  
  
-   El nombre de producto se selecciona en el cuadro de lista **Clave fija** .  
  
-   El total está seleccionado en el cuadro de lista **Valor dinámico** .  
  
-   Estos valores se van incluyendo en el cuadro **Generar columnas de salida dinámicas a partir de valores** .  
  
     [2002],[2003],[2004]  
  
## <a name="configuration-of-the-pivot-transformation"></a>Configuración de la transformación Dinámica  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden configurar en el cuadro de diálogo **Editor avanzado** , haga clic en uno de los siguientes temas:  
  
-   [Common Properties](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
## <a name="related-content"></a>Contenido relacionado  
 Para más información sobre cómo establecer las propiedades de este componente, vea [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Transformación Anulación de dinamización](pivot-transformation.md)   
 [Flujo de datos](../data-flow.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
