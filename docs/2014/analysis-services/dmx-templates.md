---
title: Plantillas DMX | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2a577e52-821d-4bd3-ba35-075a6be285c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3bf7682ce42422efb0e47e4272e53933eba92a4e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081560"
---
# <a name="dmx-templates"></a>Plantillas DMX
  Las plantillas de minería de datos ayudan a crear rápidamente consultas sofisticadas. Aunque la sintaxis general de las consultas DMX está bien documentada, el uso de plantillas facilita la creación de consultas haciendo clic y apuntando a los argumentos y orígenes de datos.  
  
## <a name="using-the-templates"></a>Usar las plantillas  
  
1.  En el cliente de minería de datos para Excel, haga clic en **consulta**.  
  
2.  En la página **Inicio** del asistente, haga clic en **siguiente**.  
  
3.  En la página, **Seleccione modelo**y haga clic en **Opciones avanzadas**.  
  
     **Sugerencia:** Si va a crear una consulta de predicción en un modelo, puede seleccionar primero el modelo y, a continuación, hacer clic en **avanzadas**, para rellenar previamente la plantilla con el nombre del modelo.  
  
4.  En el **Editor de consultas avanzadas de minería de datos**, haga clic en **plantillas DMX**y seleccione una plantilla.  
  
5.  Presione ENTRAR para cargar la plantilla en el panel Consulta DMX.  
  
6.  Siga haciendo clic en los vínculos de la plantilla y en cuanto aparezca el cuadro de diálogo, seleccione una salida, un modelo o un parámetro adecuado.  
  
     Para las consultas de predicción, elija el conjunto de datos de entrada primero y asigne después las columnas.  
  
7.  Haga clic en **Editar consulta** para cambiar a la vista del editor de texto y cambiar manualmente la consulta.  
  
     Sin embargo, tenga en cuenta que si cambia las vistas al trabajar en el editor de consultas, se borrará cualquier información que tuviera en la vista anterior. Antes de cambiar de vista, guarde el trabajo; para ello, copie y pegue las instrucciones DMX en un archivo independiente.  
  
8.  Haga clic en **Finalizar** En el cuadro de diálogo **elegir destino** , especifique dónde desea que se guarde el resultado. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Si ha ejecutado una instrucción correctamente, la instrucción DMX que envió al servidor también se registra en la ventana de **seguimiento** . Para obtener más información sobre cómo usar la característica de seguimiento, vea [seguimiento &#40;cliente de minería de datos para Excel&#41;](trace-data-mining-client-for-excel.md).  
  
 Para obtener más información sobre cómo usar el editor de consultas avanzadas de minería de datos, vea [&#40;de consultas SQL Server complementos de minería de datos&#41;](query-sql-server-data-mining-add-ins.md) y [Editor de consultas avanzadas de minería de datos](advanced-data-mining-query-editor.md).  
  
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
  
 Use estas plantillas para crear modelos o estructuras de datos personalizados. No está limitado a los modelos que admiten los asistentes: puede usar cualquier algoritmo de minería de datos admitido por la instancia [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de a la que está conectado, incluidos los algoritmos de complemento.  
  
-   Modelo de minería de datos  
  
-   Estructura de minería de datos  
  
-   Estructura de minería con datos de exclusión  
  
-   Modelo temporal  
  
-   Estructura temporal  
  
 **Propiedades del modelo**  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)  
  
  
