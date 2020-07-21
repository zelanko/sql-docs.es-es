---
title: Matriz de clasificación (complementos de minería de datos de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, validating
- classification matrix
- confusion table
- mining models, testing
ms.assetid: d6f620f4-39af-4714-9628-28ce3c361fca
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8af87605bb8c4c2cf4bcd53cce3f7ab0019b7d94
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527521"
---
# <a name="classification-matrix-sql-server-data-mining-add-ins"></a>Matriz de clasificación (Complementos de minería de datos de SQL Server)
  ![Botón Matriz de clasificación, cinta de opciones Minería de datos](media/dmc-cmatrix.gif "Botón Matriz de clasificación, cinta de opciones Minería de datos")  
  
 Puede usar la matriz de clasificación para evaluar la precisión de un modelo para la predicción. Para generar una matriz de clasificación, ejecute un conjunto de datos de prueba en el modelo; la herramienta de matriz de clasificación compara los valores reales del conjunto de pruebas con las predicciones realizadas por el modelo. Examinando la matriz, puede saber de un vistazo la frecuencia con la que el modelo es correcto y la frecuencia con la que hace predicciones incorrectas.  
  
 En estos complementos, use el Asistente para **matriz de clasificación** para seleccionar un modelo, especificar los datos de prueba y, a continuación, generar una matriz de resultados.  
  
## <a name="how-to-read-a-classification-matrix"></a>Cómo leer una matriz de clasificación  
 Supongamos que su objetivo es diseñar un programa de fidelidad del cliente y, a continuación, asignar a los clientes a las categorías adecuadas para que pueda proporcionarles el nivel de incentivos adecuado. Ha implementado tres niveles para el programa de recompensas, bronce, plata y oro, y los ha dado a los clientes en una fase de prueba. También ha diseñado un modelo que analiza los clientes y predice las categorías correctas. Ahora usará la matriz de clasificación en los datos de ensayo para determinar la calidad del modelo para predecir la oferta correcta de todos los clientes.  
  
 La tabla de la matriz de clasificación indica cuántos clientes se asignarían a cada categoría en función del modelo y compara ese resultado con el número de clientes que se suscribieron realmente a cada nivel de recompensa.  
  
||Bronce (real)|Oro (real)|Plata (real)|  
|-|-----------------------|---------------------|-----------------------|  
|Bronce|**94,45%**|15,18%|1,70 %|  
|Oro|2,72 %|**84,82%**|0.00%|  
|Plata|1,84%|0.00%|**93,80%**|  
|*Correcto*|*95,45%*|*84,82%*|*98,30%*|  
|*Incorrectas*|*4,55%*|*15,18%*|*1,70%*|  
  
-   Cada columna muestra los valores reales del conjunto de datos de prueba.  
  
-   Cada fila muestra los valores de predicción.  
  
-   Los valores en negrita, que van diagonalmente desde la esquina superior izquierda a la esquina inferior derecha de la matriz, ofrecen una idea de lo que hizo correctamente el modelo.  
  
-   Todos los demás valores fuera de la diagonal representan errores. Algunos errores son falsos positivos, lo que significa que el modelo predijo que el cliente se uniría al programa oro, pero se equivocó.  Según el dominio del que se trate, los falsos positivos pueden ser muy costosos.  
  
     Otros son falsos negativos, lo que significa que el modelo predijo que al cliente no le interesaría, aunque se unió al programa. Una vez más, según el dominio del problema, este costo de oportunidad perdida puede ser considerable.  
  
## <a name="using-the-classification-matrix-wizard"></a>Usar el Asistente para matriz de clasificación  
  
1.  Seleccione el modelo de minería de datos en el que basará las predicciones.  
  
2.  Seleccione un origen de los nuevos datos de prueba o use datos de prueba guardados con la estructura.  
  
3.  Seleccione la columna cuya precisión desea evaluar. Puede elegir solo una columna al crear una matriz, pero la columna puede tener varios valores.  
  
     Sugerencia: puede resultar difícil interpretar una matriz de clasificación si la columna de predicción tiene muchas columnas para comparar.  
  
     En la página **seleccionar columnas para predecir** , también puede especificar si desea mostrar el número de valores incorrectos e incorrectos, o bien mostrar un porcentaje.  
  
4.  En la página Seleccionar datos de origen, indique si va a usar datos de prueba externos o los datos de prueba guardados con el modelo.  
  
5.  Si usa datos de prueba externos, deberá asignar el modelo a las columnas de entrada de la página **especificar relación** del asistente.  
  
     Si usa el conjunto de datos de pruebas incrustado, la asignación se realiza automáticamente.  
  
6.  Haga clic en **Finalizar** para ejecutar predicciones en el modelo y generar la matriz de clasificación.  
  
     El asistente crea un informe que contiene la matriz de clasificación y otros detalles sobre el análisis. Este informe se guarda como una tabla en Excel, con un resumen encima del informe que indica cuántos casos se han predicho correctamente y cuántas predicciones eran incorrectas.  
  
### <a name="requirements"></a>Requisitos  
  
-   Para crear una matriz de clasificación, debe tener acceso a un modelo de minería de datos existente que admita la medida de precisión. Los modelos de pronóstico y los modelos de asociación no se pueden medir con esta herramienta.  
  
-   El modelo que va a medir necesita predecir un valor que es discreto o que ya tiene datos discretos.  
  
-   Si no ha usado la opción para guardar un conjunto de pruebas junto con la estructura o el modelo, debe obtener un conjunto de datos de entrada que tenga esencialmente el mismo número de columnas, con tipos de datos coincidentes, que los usados en el modelo.  
  
-   Tanto el modelo de minería de datos como los nuevos datos que esté usando para las pruebas deben contener al menos una columna que se pueda predecir, y las columnas deben contener el mismo tipo de datos.  
  
### <a name="known-issues"></a>Problemas conocidos  
 En SQL Server 2012 y SQL Server 2014, la capacidad para asignar el conjunto de datos de prueba interno al modelo no funciona en la herramienta de **matriz de clasificación** . Sin embargo, puede especificar un conjunto de datos externos y, a continuación, seleccionar el conjunto de entrenamiento como entrada para determinar si hay algún error en el conjunto de datos original.  
  
## <a name="see-also"></a>Consulte también  
 [Validar modelos y usar modelos para la predicción &#40;complementos de minería de datos para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)   
 [Explorar datos &#40;SQL Server complementos de minería de datos&#41;](explore-data-sql-server-data-mining-add-ins.md)   
 [Detectar categorías &#40;herramientas de análisis de tabla para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
