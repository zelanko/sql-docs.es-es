---
title: Crear una consulta de predicción Singleton desde una plantilla | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c39ff77799dd3f22f74bd03f1fc5dc0eb682a65e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-a-singleton-prediction-query-from-a-template"></a>Crear una consulta de predicción singleton desde una plantilla
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Una consulta singleton es útil cuando tiene un modelo que desea utilizar para la predicción, pero no desea asignarlo a un conjunto de datos de entrada externos o realizar predicciones masivas. Una consulta singleton le permite proporcionar un valor o varios valores al modelo y ver al momento el valor predicho.  
  
 Por ejemplo, la consulta DMX siguiente representa una consulta singleton frente al modelo de correo directo, TM_Decision_Tree.  
  
```  
SELECT * FROM [TM_Decision_tree] ;  
NATURAL PREDICTION JOIN  
(SELECT '2' AS [Number Children At Home], '45' as [Age])  
AS [t]  
```  
  
 El procedimiento siguiente describe cómo utilizar el Explorador de plantillas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para crear rápidamente esta consulta.  
  
### <a name="to-open-the-analysis-services-templates-in-sql-server-management-studio"></a>Abrir las plantillas de Analysis Services en SQL Server Management Studio  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el menú **Ver** , haga clic en el **Explorador de plantillas**.  
  
2.  Haga clic en el icono de cubo para abrir las plantillas de **Analysis Server**.  
  
### <a name="to-open-a-prediction-query-template"></a>Abrir una plantilla de consulta de predicción  
  
1.  En el **Explorador de plantillas**, en la lista de plantillas de Analysis Server, expanda **DMX**y, luego, expanda **Consultas de predicción**.  
  
2.  Haga doble clic en **Predicción de singleton**.  
  
3.  En el cuadro de diálogo **Conectar a Analysis Services** , escriba el nombre del servidor que tiene la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene el modelo de minería de datos que se va a consultar.  
  
4.  Haga clic en **Conectar**.  
  
5.  La plantilla se abre en la base de datos especificada junto con un Explorador de objetos del modelo de minería de datos que contiene las funciones de minería de datos y una lista de estructuras de minería de datos y los modelos relacionados.  
  
### <a name="to-customize-the-singleton-query-template"></a>Personalizar la plantilla de consulta singleton  
  
1.  En la plantilla, haga clic en la lista desplegable **Bases de datos disponibles** y, después, seleccione una instancia de Analysis Services en la lista.  
  
2.  En la lista **Modelo de minería de datos** , seleccione el modelo de minería de datos que desea consultar.  
  
     La lista de columnas del modelo de minería de datos aparece en el panel **Metadatos** del explorador de objetos.  
  
3.  En el menú **Consulta** , seleccione **Especificar valores para parámetros de plantilla**.  
  
4.  En la fila **seleccionar lista** , escriba * para devolver todas las columnas o escriba una lista delimitada por comas de columnas y expresiones para devolver columnas concretas.  
  
     Si escribe *, se devuelve la columna de predicción, junto con cualquier columna para la que proporciona nuevos valores en el paso 6.  
  
     Para el código de ejemplo mostrado al inicio de este tema, la fila **seleccionar lista** se ha definido en *.  
  
5.  En la fila **modelo de minería de datos** , escriba el nombre del modelo de minería de datos entre la lista de modelos de minería de datos que aparecen en el **Explorador de objetos**.  
  
     Para el código de ejemplo mostrado al inicio de este tema, la fila **modelo de minería de datos** se ha establecido en el nombre **TM_Decision_Tree**.  
  
6.  En la fila **value** , escriba el nuevo valor de datos para el que desea realizar una predicción.  
  
     En el caso del código que se muestra en el inicio de este tema, la fila **value** se definió en **2** para predecir el comportamiento de compras según la cantidad de niños en casa.  
  
7.  En la fila **column** , escriba el nombre de la columna del modelo de minería de datos al que deberían estar asignados los nuevos datos.  
  
     Para el código de ejemplo mostrado en el inicio de este tema, la fila **column** se definió en **Number Children at Home**.  
  
    > [!NOTE]  
    >  Al usar el cuadro de diálogo **Especificar valores para parámetros de plantilla** , no tiene que agregar corchetes al nombre de columna. Los corchetes se agregarán automáticamente.  
  
8.  Deje el **input alias** como **t**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. En el panel de texto de consulta, busque las marcas en zigzag rojas debajo de la coma y los puntos suspensivos que indican un error de sintaxis. Elimine los puntos suspensivos y agregue cualquier condición de consulta adicional que desee. Si no agrega ninguna otra condición, elimine la coma.  
  
     Para el código de ejemplo mostrado al inicio de este tema, la condición de consulta adicional se ha establecido en **'45' as [Age]**.  
  
11. Haga clic en **Ejecutar**.  
  
## <a name="see-also"></a>Vea también  
 [Crear predicciones & #40; Tutorial de minería de datos básicos & #41;](http://msdn.microsoft.com/library/a8410ed2-bb98-4d51-a9eb-b239be1201c2)  
  
  
