---
title: Crear predicciones (Tutorial de minería de datos básicos) | Microsoft Docs
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
ms.sourcegitcommit: d9c5b9ab3c282775ed61712892eeb3e150ccc808
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67597526"
---
# <a name="creating-predictions-basic-data-mining-tutorial"></a>Crear predicciones (Tutorial básico de minería de datos)
  Después de haber probado la precisión de los modelos de minería de datos y esté satisfecho con los resultados, a continuación, puede generar predicciones con el generador de consultas de predicción en el **predicción de modelo de minería de datos** ficha en la minería de datos Diseñador.  
  
 El Generador de consultas de predicción tiene tres vistas. Con el **diseño** y **consulta** vistas, puede generar y examinar una consulta. A continuación, puede ejecutar la consulta y ver los resultados en el **resultado** vista.  
  
 Todas las consultas de predicción utilizan DMX, que es el acrónimo del lenguaje de Extensiones de minería de datos (DMX). DMX tiene una sintaxis similar a la de T-SQL, pero se utiliza con consultas en objetos de minería de datos. Aunque la sintaxis de DMX no es complicado, con un generador de consultas como este, o en el [SQL Server Data Mining Add-Ins para Office](../../2014/analysis-services/data-mining/sql-server-data-mining-add-ins-for-office.md), resulta mucho más fácil seleccionar entradas y generar expresiones, por lo que se recomienda encarecidamente que aprenda los aspectos básicos.  
  
## <a name="creating-the-query"></a>Crear la consulta  
 El primer paso para crear una consulta de predicción consiste en seleccionar un modelo de minería de datos y una tabla de entrada.  
  
#### <a name="to-select-a-model-and-input-table"></a>Para seleccionar un modelo de minería de datos y una tabla de entrada  
  
1.  En el **predicción de modelo de minería de datos** ficha del Diseñador de minería de datos, en el **Mining Model** cuadro, haga clic en **Seleccionar modelo**.  
  
2.  En el **Seleccionar modelo de minería de datos** diálogo cuadro, vaya a través del árbol a la **Targeted Mailing** estructura, expanda la estructura, seleccione `TM_Decision_Tree`y, a continuación, haga clic en **Aceptar**.  
  
3.  En el **Seleccionar tabla (s) de entrada** cuadro, haga clic en **Seleccionar tabla de casos**.  
  
4.  En el **Seleccionar tabla** cuadro de diálogo el **origen de datos** lista, seleccione la vista del origen de datos [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)].  
  
5.  En **nombre de tabla o vista**, seleccione el **ProspectiveBuyer (dbo)** de tabla y, a continuación, haga clic en **Aceptar**.  
  
     El `ProspectiveBuyer` más se parezca la tabla el **vTargetMail** tabla de casos.  
  
## <a name="mapping-the-columns"></a>Asignar las columnas  
 Después de seleccionar la tabla de entrada, el Generador de consultas de predicción crea una asignación predeterminada entre el modelo de minería de datos y la tabla de entrada, en función de los nombres de las columnas. Al menos una columna de la estructura debe coincidir con una columna de los datos externos.  
  
> [!IMPORTANT]  
>  Los datos que use para determinar la precisión de los modelos deben contener una columna que se pueda asignar a la columna de predicción. Si no existe esa columna, puede crear una con valores vacíos, pero debe tener el mismo tipo de datos que la columna de predicción.  
  
#### <a name="to-map-the-inputs-to-the-model"></a>Para asignar las entradas al modelo  
  
1.  Haga clic en las líneas que conectan el **Mining Model** ventana a la **Seleccionar tabla de entrada** ventana y seleccione **modificar conexiones**.  
  
     Observe que no todas las columnas están asignadas. Agregaremos asignaciones para varias **columnas de la tabla**. También generaremos una columna de fecha de nacimiento nueva en función de la columna de fecha actual, para que la coincidencia de las columnas sea mejor.  
  
2.  En **columna de tabla**, haga clic en el `Bike Buyer` de celda y seleccione ProspectiveBuyer.Unknown en la lista desplegable.  
  
     De esta forma se asigna la columna de predicción, [Bike Buyer], a una columna de la tabla de entrada.  
  
3.  Haga clic en **Aceptar**.  
  
4.  En **el Explorador de soluciones**, haga clic en el **Targeted Mailing** vista del origen de datos y seleccione **Diseñador de vistas**.  
  
5.  Haga clic en la tabla ProspectiveBuyer y seleccione **nuevo cálculo con nombre**.  
  
6.  En el **crear cálculo con nombre** cuadro de diálogo para **nombre de columna**, tipo `calcAge`.  
  
7.  Para **descripción**, tipo **calcular la edad en función de la fecha de nacimiento**.  
  
8.  En el **expresión** , escriba `DATEDIFF(YYYY,[BirthDate],getdate())` y, a continuación, haga clic en **Aceptar**.  
  
     Dado que la tabla de entrada no tiene ningún **Age** columna correspondiente a la que se muestra en el modelo, puede utilizar esta expresión para calcular la edad del cliente de la columna de fecha de nacimiento de la tabla de entrada. Puesto que **edad** se identificó como más influyentes columna para predecir la compra de bicicletas, debe existir en el modelo y en la tabla de entrada.  
  
9. En el Diseñador de minería de datos, seleccione el **predicción de modelo de minería de datos** pestaña y vuelva a abrir el **modificar conexiones** ventana.  
  
10. En **columna de tabla**, haga clic en el **Age** de celda y seleccione ProspectiveBuyer.calcAge en la lista desplegable.  
  
    > [!WARNING]  
    >  Si no ve la columna en la lista, puede que tenga que actualizar la definición de la vista del origen de datos que se ha cargado en el diseñador. Para ello, desde el **archivo** menú, seleccione **guardar todo**y, a continuación, cierre y vuelva a abrir el proyecto en el diseñador.  
  
11. Haga clic en **Aceptar**.  
  
## <a name="designing-the-prediction-query"></a>Diseñar la consulta de predicción  
  
1.  El primer botón de la barra de herramientas de la **predicción de modelo de minería de datos** pestaña es la **cambiar al diseño ver / cambiar a vista de resultado / cambiar a vista consulta** botón. Haga clic en la flecha hacia abajo en este botón y seleccione **diseño**.  
  
2.  En la cuadrícula en el **predicción de modelo de minería de datos** pestaña, haga clic en la celda de la primera fila vacía en el **origen** columna y, a continuación, seleccione **función de predicción**.  
  
3.  En el **función de predicción** de fila, en el **campo** columna, seleccione `PredictProbability`.  
  
     En el **Alias** columna de la misma fila, tipo **probabilidad del resultado**.  
  
4.  Desde el **Mining Model** ventana anterior, seleccione y arrastre [Bike Buyer] a la **criterios o argumento** celda.  
  
     Cuando suelte, [TM_Decision_Tree]. [Bike Buyer] aparece en el **criterios o argumento** celda.  
  
     De esta forma, se especificará la columna de destino para la función `PredictProbability`. Para obtener más información acerca de las funciones, vea [extensiones de minería de datos &#40;DMX&#41; referencia de funciones](/sql/dmx/data-mining-extensions-dmx-function-reference).  
  
5.  Haga clic en la siguiente fila vacía en el **origen** columna y, a continuación, seleccione **TM_Decision_Tree** modelo de minería de datos.  
  
6.  En el `TM_Decision_Tree` de fila, en el **campo** columna, seleccione `Bike Buyer`.  
  
7.  En el `TM_Decision_Tree` de fila, en el **criterios o argumento** columna, escriba `=1`.  
  
8.  Haga clic en la siguiente fila vacía en el **origen** columna y, a continuación, seleccione **tabla ProspectiveBuyer**.  
  
9. En el `ProspectiveBuyer` de fila, en el **campo** columna, seleccione **ProspectiveBuyerKey**.  
  
     De esta forma, se agregará el identificador único a la consulta de predicción para que pueda identificar quién es más y menos probable que compre una bicicleta.  
  
10. Agregue cinco filas más a la cuadrícula. Para cada fila, seleccione **tabla ProspectiveBuyer** como el **origen** y, a continuación, agregue las siguientes columnas de la **campo** celdas:  
  
    -   calcAge  
  
    -   LastName  
  
    -   FirstName  
  
    -   AddressLine1  
  
    -   AddressLine2  
  
 Finalmente, ejecute la consulta y examine los resultados.  
  
 El **generador de consultas de predicción** también incluye estos controles:  
  
-   **Mostrar** casilla de verificación  
  
     Permite quitar cláusulas de la consulta sin tener que eliminarlas desde el diseñador. Esto puede resultar útil cuando se trabaja con consultas complejas y se desear conservar la sintaxis sin tener que copiar y pegar DMX en la ventana.  
  
-   **Grupo**  
  
     Inserta un paréntesis de apertura (izquierdo) al principio de la línea seleccionada o inserta un paréntesis de cierre (derecho) al final de la línea actual.  
  
-   **O**  
  
     Inserta el operador `AND` o el operador `OR` inmediatamente después de la función o columna actual.  
  
#### <a name="to-run-the-query-and-view-results"></a>Para ejecutar la consulta y ver los resultados  
  
1.  En el **predicción de modelo de minería de datos** ficha, seleccione el **resultado** botón.  
  
2.  Una vez que la consulta se ejecute y se muestren los resultados, puede revisarlos.  
  
     El **predicción de modelo de minería de datos** ficha muestra información de contacto de clientes potenciales que suelen ser los compradores de bicicletas. El **probabilidad del resultado** columna indica la probabilidad de que la predicción sea correcta. Puede utilizar estos resultados para determinar a qué clientes potenciales debe dirigirse en el correo.  
  
3.  En este punto, puede guardar los resultados. Tiene tres opciones:  
  
    -   Haga clic en una fila de datos en los resultados y seleccione **copia** para guardar solo el valor (y el encabezado de columna) en el Portapapeles.  
  
    -   Haga clic en cualquier fila de los resultados y seleccione **copiar todo** para copiar el conjunto de resultados completo, incluidos los encabezados de columna, en el Portapapeles.  
  
    -   Haga clic en **Guardar resultado de consulta** para guardar los resultados directamente a una base de datos como sigue:  
  
        1.  En el **Guardar resultado de consulta de minería de datos** cuadro de diálogo, seleccione un origen de datos o definir un nuevo origen de datos.  
  
        2.  Escriba un nombre para la tabla que contendrá los resultados de la consulta.  
  
        3.  Utilice la opción **agregar a DSV**, para crear la tabla y agregarla a una vista del origen de datos existente. Esto es útil si desea conservar todas las tablas relacionadas para un modelo, como datos de entrenamiento, datos de origen de predicción y consulta los resultados de la misma vista del origen de datos.  
  
        4.  Utilice la opción **sobrescribir si existe**, para actualizar una tabla existente con los resultados más recientes.  
  
             Debe utilizar la opción de sobrescribir la tabla si ha agregado algunas columnas a la consulta de predicción, cambiado los nombres o los tipos de datos de las columnas en la consulta de predicción, o si ha ejecutado alguna instrucción ALTER en la tabla de destino.  
  
             Además, si varias columnas tienen el mismo nombre (por ejemplo, el nombre de columna predeterminado **expresión**) debe crear un alias para las columnas con nombres duplicados, o se producirá un error cuando el diseñador intente guardar los resultados en SQL Servidor. La razón es que SQL Server no permite que varias columnas tengan el mismo nombre.  
  
             Para obtener más información, consulte [Data Mining consulta resultado cuadro de diálogo Guardar &#40;vista predicción de modelo de minería de datos&#41;](../../2014/analysis-services/save-data-mining-query-result-dialog-box-mining-model-prediction-view.md).  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Con la obtención de detalles en datos de estructura &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/using-drillthrough-on-structure-data-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear una consulta de predicción con el Generador de consultas de predicción](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
