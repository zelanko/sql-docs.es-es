---
title: Crear predicciones (tutorial básico de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a8410ed2-bb98-4d51-a9eb-b239be1201c2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 456aec6c6b9d0d1a5d0ee1d9949507a37577130c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67597526"
---
# <a name="creating-predictions-basic-data-mining-tutorial"></a>Crear predicciones (Tutorial básico de minería de datos)
  Después de probar la precisión de los modelos de minería de datos y decidir que está satisfecho con los resultados, puede generar predicciones mediante el Generador de consultas de predicción en la pestaña **predicción de modelo de minería** de datos del diseñador de minería de datos.  
  
 El Generador de consultas de predicción tiene tres vistas. Con las vistas **diseño** y **consulta** , puede compilar y examinar la consulta. Después, puede ejecutar la consulta y ver los resultados en la vista de **resultados** .  
  
 Todas las consultas de predicción utilizan DMX, que es el acrónimo del lenguaje de Extensiones de minería de datos (DMX). DMX tiene una sintaxis similar a la de T-SQL, pero se utiliza con consultas en objetos de minería de datos. Aunque la sintaxis DMX no es complicada, el uso de un generador de consultas como este, o el de los [Complementos de minería de datos SQL Server para Office](../../2014/analysis-services/data-mining/sql-server-data-mining-add-ins-for-office.md), facilita la selección de entradas y expresiones de compilación, por lo que se recomienda encarecidamente conocer los aspectos básicos.  
  
## <a name="creating-the-query"></a>Crear la consulta  
 El primer paso para crear una consulta de predicción consiste en seleccionar un modelo de minería de datos y una tabla de entrada.  
  
#### <a name="to-select-a-model-and-input-table"></a>Para seleccionar un modelo de minería de datos y una tabla de entrada  
  
1.  En la pestaña **predicción de modelo de minería** de datos del diseñador de minería de datos, en el cuadro modelo de **minería** de datos, haga clic en **Seleccionar modelo**.  
  
2.  En el cuadro de diálogo **Seleccionar modelo de minería de datos** , desplácese por el árbol hasta la estructura de **correo** de destino `TM_Decision_Tree`, expanda la estructura, seleccione y, a continuación, haga clic en **Aceptar**.  
  
3.  En el cuadro **seleccionar tabla (s) de entrada** , haga clic en **seleccionar tabla de casos**.  
  
4.  En el cuadro de diálogo **seleccionar tabla** , en la lista **origen de datos** , seleccione la vista [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]del origen de datos.  
  
5.  En **nombre de tabla o vista**, seleccione la tabla **ProspectiveBuyer (DBO)** y, a continuación, haga clic en **Aceptar**.  
  
     La `ProspectiveBuyer` tabla es muy similar a la tabla de casos **vTargetMail** .  
  
## <a name="mapping-the-columns"></a>Asignar las columnas  
 Después de seleccionar la tabla de entrada, el Generador de consultas de predicción crea una asignación predeterminada entre el modelo de minería de datos y la tabla de entrada, en función de los nombres de las columnas. Al menos una columna de la estructura debe coincidir con una columna de los datos externos.  
  
> [!IMPORTANT]  
>  Los datos que use para determinar la precisión de los modelos deben contener una columna que se pueda asignar a la columna de predicción. Si no existe esa columna, puede crear una con valores vacíos, pero debe tener el mismo tipo de datos que la columna de predicción.  
  
#### <a name="to-map-the-inputs-to-the-model"></a>Para asignar las entradas al modelo  
  
1.  Haga clic con el botón secundario en las líneas que conectan la ventana **modelo de minería de datos** a la ventana **seleccionar tabla de entrada** y seleccione **modificar conexiones**.  
  
     Observe que no todas las columnas están asignadas. Agregaremos asignaciones para varias columnas de la **tabla**. También generaremos una columna de fecha de nacimiento nueva en función de la columna de fecha actual, para que la coincidencia de las columnas sea mejor.  
  
2.  En **columna**de la tabla, `Bike Buyer` haga clic en la celda y seleccione ProspectiveBuyer. Unknown en la lista desplegable.  
  
     De esta forma se asigna la columna de predicción, [Bike Buyer], a una columna de la tabla de entrada.  
  
3.  Haga clic en **OK**.  
  
4.  En **Explorador de soluciones**, haga clic con el botón secundario en la vista del origen de datos **Targeted mailing** y seleccione **Diseñador de vistas**.  
  
5.  Haga clic con el botón secundario en la tabla ProspectiveBuyer y seleccione **nuevo cálculo con nombre**.  
  
6.  En el cuadro de diálogo **crear cálculo con nombre** , en **nombre**de `calcAge`columna, escriba.  
  
7.  En **Descripción**, escriba **Calculate Age based on FechaNacimiento**.  
  
8.  En el cuadro **expresión** , escriba `DATEDIFF(YYYY,[BirthDate],getdate())` y, a continuación, haga clic en **Aceptar**.  
  
     Dado que la tabla de entrada no tiene ninguna columna **Age** que se corresponda con la del modelo, puede utilizar esta expresión para calcular la edad del cliente a partir de la columna FechaNacimiento de la tabla de entrada. Como la **edad** se identificó como la columna más influyente para predecir la compra de bicicletas, debe existir en el modelo y en la tabla de entrada.  
  
9. En el diseñador de minería de datos, seleccione la pestaña **predicción de modelo de minería** de datos y vuelva a abrir la ventana **modificar conexiones** .  
  
10. En **columna**de la tabla, haga clic en la celda **Age** y seleccione ProspectiveBuyer. Calc en la lista desplegable.  
  
    > [!WARNING]  
    >  Si no ve la columna en la lista, puede que tenga que actualizar la definición de la vista del origen de datos que se ha cargado en el diseñador. Para ello, en el menú **archivo** , seleccione **guardar todo**y, a continuación, cierre y vuelva a abrir el proyecto en el diseñador.  
  
11. Haga clic en **OK**.  
  
## <a name="designing-the-prediction-query"></a>Diseñar la consulta de predicción  
  
1.  El primer botón de la barra de herramientas de la pestaña **predicción de modelo de minería de datos** es el botón **cambiar a vista de diseño/cambiar a vista de resultado/cambiar a vista de consulta** . Haga clic en la flecha hacia abajo de este botón y seleccione **diseño**.  
  
2.  En la cuadrícula de la pestaña **predicción de modelo de minería de datos** , haga clic en la celda de la primera fila vacía de la columna **origen** y, a continuación, seleccione **función de predicción**.  
  
3.  En la fila **función de predicción** , en la columna **campo** , `PredictProbability`seleccione.  
  
     En la columna **alias** de la misma fila, escriba **probabilidad de resultado**.  
  
4.  En la ventana **modelo de minería de datos** anterior, seleccione y arrastre [Bike Buyer] a la celda **criterios o argumento** .  
  
     Cuando lo permita, [TM_Decision_Tree]. [Bike Buyer] aparece en la celda **criterios o argumento** .  
  
     De esta forma, se especificará la columna de destino para la función `PredictProbability`. Para obtener más información acerca de las funciones, consulte [extensiones de minería de datos &#40;referencia de funciones DMX&#41;](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
5.  Haga clic en la siguiente fila vacía de la columna **origen** y, a continuación, seleccione **TM_Decision_Tree** modelo de minería de datos.  
  
6.  En la `TM_Decision_Tree` fila, en la columna **campo** , seleccione `Bike Buyer`.  
  
7.  En la `TM_Decision_Tree` fila, en la columna **criterios o argumento** , escriba `=1`.  
  
8.  Haga clic en la siguiente fila vacía de la columna **origen** y, a continuación, seleccione **tabla ProspectiveBuyer**.  
  
9. En la `ProspectiveBuyer` fila, en la columna **campo** , seleccione **ProspectiveBuyerKey**.  
  
     De esta forma, se agregará el identificador único a la consulta de predicción para que pueda identificar quién es más y menos probable que compre una bicicleta.  
  
10. Agregue cinco filas más a la cuadrícula. En cada fila, seleccione la **tabla ProspectiveBuyer** como **origen** y, a continuación, agregue las columnas siguientes en las celdas **campo** :  
  
    -   calcAge  
  
    -   Apellidos  
  
    -   Nombre  
  
    -   AddressLine1  
  
    -   AddressLine2  
  
 Finalmente, ejecute la consulta y examine los resultados.  
  
 La **predicción generador de consultas** también incluye estos controles:  
  
-   **Mostrar** casilla  
  
     Permite quitar cláusulas de la consulta sin tener que eliminarlas desde el diseñador. Esto puede resultar útil cuando se trabaja con consultas complejas y se desear conservar la sintaxis sin tener que copiar y pegar DMX en la ventana.  
  
-   **Grupo**  
  
     Inserta un paréntesis de apertura (izquierdo) al principio de la línea seleccionada o inserta un paréntesis de cierre (derecho) al final de la línea actual.  
  
-   **Y/O**  
  
     Inserta el operador `AND` o el operador `OR` inmediatamente después de la función o columna actual.  
  
#### <a name="to-run-the-query-and-view-results"></a>Para ejecutar la consulta y ver los resultados  
  
1.  En la pestaña **predicción de modelo de minería de datos** , seleccione el botón **resultado** .  
  
2.  Una vez que la consulta se ejecute y se muestren los resultados, puede revisarlos.  
  
     La pestaña **predicción de modelo de minería de datos** muestra información de contacto de los clientes potenciales que probablemente sean compradores de bicicletas. La columna **probabilidad de resultado** indica la probabilidad de que la predicción sea correcta. Puede utilizar estos resultados para determinar a qué clientes potenciales debe dirigirse en el correo.  
  
3.  En este punto, puede guardar los resultados. Tiene tres opciones:  
  
    -   Haga clic con el botón secundario en una fila de datos de los resultados y seleccione **copiar** para guardar solo ese valor (y el encabezado de columna) en el portapapeles.  
  
    -   Haga clic con el botón secundario en cualquier fila de los resultados y seleccione **copiar todo** para copiar todo el conjunto de resultados, incluidos los encabezados de columna, en el portapapeles.  
  
    -   Haga clic en **Guardar resultado** de la consulta para guardar los resultados directamente en una base de datos de la siguiente manera:  
  
        1.  En el cuadro de diálogo **Guardar resultado de consulta de minería de datos** , seleccione un origen de datos o defina un nuevo origen de datos.  
  
        2.  Escriba un nombre para la tabla que contendrá los resultados de la consulta.  
  
        3.  Use la opción **Agregar a DSV**para crear la tabla y agregarla a una vista del origen de datos existente. Esto resulta útil si desea conservar todas las tablas relacionadas para un modelo, como los datos de entrenamiento, los datos de origen de la predicción y los resultados de la consulta, en la misma vista del origen de datos.  
  
        4.  Use la opción **sobrescribir si existe**, para actualizar una tabla existente con los resultados más recientes.  
  
             Debe utilizar la opción de sobrescribir la tabla si ha agregado algunas columnas a la consulta de predicción, cambiado los nombres o los tipos de datos de las columnas en la consulta de predicción, o si ha ejecutado alguna instrucción ALTER en la tabla de destino.  
  
             Además, si varias columnas tienen el mismo nombre (por ejemplo, la **expresión**de nombre de columna predeterminada), debe crear un alias para las columnas con nombres duplicados, o se producirá un error cuando el diseñador intente guardar los resultados en SQL Server. La razón es que SQL Server no permite que varias columnas tengan el mismo nombre.  
  
             Para obtener más información, vea [cuadro de diálogo Guardar resultado de consulta de minería de datos &#40;vista predicción de modelo de minería de datos&#41;](../../2014/analysis-services/save-data-mining-query-result-dialog-box-mining-model-prediction-view.md).  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Usar la obtención de detalles en datos de estructura &#40;tutorial básico de minería de datos&#41;](../../2014/tutorials/using-drillthrough-on-structure-data-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Consulte también  
 [Crear una consulta de predicción con el Generador de consultas de predicción](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
