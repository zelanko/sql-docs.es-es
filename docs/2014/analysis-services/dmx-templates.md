---
title: Plantillas DMX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 2a577e52-821d-4bd3-ba35-075a6be285c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7e3bee7fa85c98e50fdb940d2dfb23f76f3a462c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731762"
---
# <a name="dmx-templates"></a>Plantillas DMX
  Las plantillas de minería de datos ayudan a crear rápidamente consultas sofisticadas. Aunque la sintaxis general de las consultas DMX está bien documentada, el uso de plantillas facilita la creación de consultas haciendo clic y apuntando a los argumentos y orígenes de datos.  
  
## <a name="using-the-templates"></a>Usar las plantillas  
  
1.  En el cliente de minería de datos para Excel, haga clic en **consulta**.  
  
2.  En el Asistente para **iniciar** página, haga clic en **siguiente**.  
  
3.  En la página, **Seleccionar modelo**, haga clic en **avanzadas**.  
  
     **Sugerencia:** Si va a crear una consulta de predicción en un modelo, puede seleccionar el modelo primero y, a continuación, haga clic en **avanzadas**, para rellenar previamente la plantilla con el nombre del modelo.  
  
4.  En el **Editor minería de datos avanzada consulta**, haga clic en **plantillas DMX**y seleccione una plantilla.  
  
5.  Presione ENTRAR para cargar la plantilla en el panel Consulta DMX.  
  
6.  Siga haciendo clic en los vínculos de la plantilla y en cuanto aparezca el cuadro de diálogo, seleccione una salida, un modelo o un parámetro adecuado.  
  
     Para las consultas de predicción, elija el conjunto de datos de entrada primero y asigne después las columnas.  
  
7.  Haga clic en **Editar consulta** para cambiar a la vista del editor de texto y cambie manualmente la consulta.  
  
     Sin embargo, tenga en cuenta que si cambia las vistas al trabajar en el editor de consultas, se borrará cualquier información que tuviera en la vista anterior. Antes de cambiar de vista, guarde el trabajo; para ello, copie y pegue las instrucciones DMX en un archivo independiente.  
  
8.  Haga clic en **Finalizar**. En el **elegir destino** diálogo cuadro, especifique dónde desea que se guarden los resultados. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Si ha ejecutado una instrucción correctamente, la instrucción DMX que envía al servidor también se registra en el **seguimiento** ventana. Para obtener más información sobre cómo usar la característica de seguimiento, vea [seguimiento &#40;cliente de minería de datos para Excel&#41;](trace-data-mining-client-for-excel.md).  
  
 Para obtener más información sobre cómo usar los datos de minería de datos Editor de consultas avanzadas, vea [consulta &#40;complementos de minería de datos de SQL Server&#41; ](query-sql-server-data-mining-add-ins.md) y [Editor de consultas avanzadas de minería de datos](advanced-data-mining-query-editor.md).  
  
## <a name="list-of-dmx-templates"></a>Lista de plantillas DMX  
 En el Cliente de minería de datos para Excel se incluyen las siguientes plantillas DMX.  
  
 **Predicción**  
  
 Use estas plantillas para crear consultas de predicción avanzadas, incluidas las consultas no admitidas por los asistentes de los complementos, como consultas que usan tablas anidadas u orígenes de datos externos.  
  
-   Predicciones filtradas  
  
-   Predicciones anidadas y filtradas  
  
-   Predicciones anidadas  
  
-   Predicción de singleton  
  
-   Predicciones estándar  
  
-   Predicciones de series temporales  
  
-   Consulta de predicción TOP  
  
-   Consulta de predicción TOP en tabla anidada  
  
 **Crear**  
  
 Use estas plantillas para crear modelos o estructuras de datos personalizados. No se limita a los modelos admitidos por los asistentes; puede usar cualquier algoritmo de minería de datos admitido por la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que están conectados, incluidos los algoritmos de complemento.  
  
-   Modelo de minería de datos  
  
-   Estructura de minería de datos  
  
-   Estructura de minería con datos de exclusión  
  
-   Modelo temporal  
  
-   Estructura temporal  
  
 **Propiedades de modelo**  
  
 Use estas plantillas para crear consultas que obtienen metadatos sobre el modelo y el conjunto de entrenamiento. También puede recuperar detalles del contenido del modelo u obtener un perfil estadístico de los datos de entrenamiento.  
  
-   Contenido del modelo de minería de datos  
  
-   Valores de columna mínimos y máximos  
  
-   Casos de prueba/entrenamiento de estructura de minería  
  
-   Valores de columna discreta  
  
 **Administración**  
  
 Use estas plantillas para realizar cualquier tarea de administración admitida por DMX, lo que incluye importar y exportar modelos, eliminar modelos y borrar modelos o estructuras de datos.  
  
-   Borrar modelo de minería de datos  
  
-   Borrar estructura y modelos  
  
-   Borrar estructura de minería  
  
-   Eliminar modelo de minería de datos  
  
-   Eliminar estructura de minería  
  
-   Cambiar nombre del modelo de minería de datos  
  
-   Cambiar nombre de la estructura de minería  
  
-   Entrenar modelo de minería de datos  
  
-   Entrenar estructura de minería anidada  
  
-   Entrenar estructura de minería  
  
### <a name="requirements"></a>Requisitos  
 Dependiendo de la plantilla que esté utilizando, es posible que necesite permisos administrativos para tener acceso al servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y ejecutar la consulta.  
  
## <a name="see-also"></a>Vea también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)  
  
  
