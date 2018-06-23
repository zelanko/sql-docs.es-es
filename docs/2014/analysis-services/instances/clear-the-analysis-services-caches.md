---
title: Borrar las Analysis Services las memorias caché | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6bf66fdd-6a03-4cea-b7e2-eb676ff276ff
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 02a7a6620927472b0019cb4d23a3695f02dd7138
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36114152"
---
# <a name="clear-the-analysis-services-caches"></a>Borrar las memorias caché de Analysis Services
  Analysis Services almacena los datos en memoria caché para mejorar el rendimiento de las consultas. En este tema se proporcionan recomendaciones para usar el comando ClearCache de XMLA con el fin de borrar las memorias caché creadas en respuesta a una consulta MDX. Los efectos de ejecutar ClearCache varían dependiendo de que se use un modelo tabular o multidimensional.  
  
 **Cuándo conviene borrar la memoria caché para los modelos multidimensionales**  
  
 Para las bases de datos multidimensionales, Analysis Services genera memorias caché en el motor de fórmulas durante la evaluación de un cálculo y en el motor de almacenamiento para los resultados de las consultas de dimensión y de grupo de medida. Las consultas de grupo de medida se producen cuando el motor de fórmulas necesita datos de medida para un subcubo o una coordenada de celda. Las consultas de dimensión se producen cuando se consultan jerarquías no naturales y cuando se aplica autoexist.  
  
 Se recomienda borrar la memoria caché al realizar pruebas de rendimiento. La acción de borrar la memoria caché entre ejecuciones de pruebas garantiza que el almacenamiento en memoria caché no sesga los resultados de pruebas que miden el impacto de un cambio en el diseño de la consulta.  
  
 **Cuándo conviene borrar la memoria caché para los modelos tabulares**  
  
 Los modelos tabulares se almacenan normalmente en memoria, donde se realizan agregaciones y otros cálculos en el momento de ejecutar una consulta. En sí, el comando ClearCache tiene un efecto limitado en los modelos tabulares. En un modelo tabular, los datos se pueden agregar a las memorias caché de Analysis Services si se ejecutan consultas MDX en él. Concretamente, las medidas de DAX a que hacen referencia las operaciones de autoexist y MDX pueden almacenar los resultados en la memoria caché de fórmulas y en la memoria caché de dimensiones, respectivamente. Sin embargo, conviene tener en cuenta que las jerarquías no naturales y las consultas de grupo de medidas no almacenan en caché los resultados del motor de almacenamiento. Además, es importante reconocer que las consultas de DAX no almacenan en caché los resultados del motor de fórmulas y de almacenamiento. En la medida en que las memorias caché existen como resultado de consultas MDX, la ejecución de ClearCache en un modelo tabular invalidará los datos almacenados en caché del sistema.  
  
 Al ejecutar ClearCache también se borrarán las memorias caché en memoria en el motor analítico en memoria xVelocity (VertiPaq). El motor xVelocity mantiene un pequeño conjunto de resultados almacenados en caché. La ejecución de ClearCache invalidará estas memorias caché en el motor xVelocity.  
  
 Por último, la ejecución de ClearCache también quitará los datos residuales que queden en memoria cuando se vuelve a configurar un modelo tabular para `DirectQuery` modo. Esto es especialmente importante si el modelo contiene información confidencial sujeta a controles estrictos. En este caso, la ejecución de ClearCache es una acción preventiva que se puede adoptar para asegurarse de que solo existe información confidencial donde se espera que esté. La acción de borrar la memoria caché manualmente es necesaria si se usa [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para implementar el modelo y cambiar el modo de consulta. En cambio, si se usa [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para especificar `DirectQuery` en el modelo y las particiones, se borrará automáticamente la memoria caché cuando cambie el modelo para utilizar ese modo de consulta.  
  
 En comparación con las recomendaciones para borrar las memorias caché de modelos multidimensionales durante las pruebas de rendimiento, no hay ninguna recomendación general para borrar las memorias caché de modelos tabulares. Si no está administrando la implementación de un modelo tabular que contiene información confidencial, no hay ninguna tarea administrativa específica que requiera borrar la memoria caché.  
  
## <a name="clear-the-cache-for-analysis-services-models"></a>Borrar la memoria caché para los modelos de Analysis Services  
 Para borrar la memoria caché, use XMLA y [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Puede borrar la memoria caché en el nivel de base de datos, cubo, dimensión o tabla, o grupo de medida. Los pasos siguientes para borrar la memoria caché en el nivel de base de datos son aplicables a los modelos tanto multidimensionales como tabulares.  
  
> [!NOTE]  
>  Las pruebas de rendimiento rigurosas pueden requerir un enfoque más completo para borrar la memoria caché. Para obtener instrucciones sobre cómo vaciar las memorias caché de Analysis Services y del sistema, vea la sección sobre borrado de memorias caché en la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?linkID=http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 En los modelos multidimensionales y tabulares, la acción de borrar algunas de estas memorias caché puede ser un proceso de dos pasos que consiste en invalidar la memoria caché cuando se ejecuta ClearCache, seguido de vaciarla cuando se recibe la consulta siguiente. Una reducción del consumo de memoria solo se manifestará después de que la memoria caché quede realmente vacía.  
  
 La acción de borrar la memoria caché requiere proporcionar un identificador de objeto a la instrucción `ClearCache` en una consulta XMLA. En el primer paso de este tema se explica cómo obtener un identificador de objeto.  
  
#### <a name="step-1-get-the-object-identifier"></a>Paso 1: obtener el identificador de objeto  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], haga clic con el botón derecho en un objeto, seleccione **Propiedades**y copie el valor de la propiedad ID en el panel **Propiedades** . Este enfoque funciona para una base de datos, cubo, dimensión o tabla.  
  
2.  Para obtener el identificador de grupo de medida, haga clic con el botón derecho en el grupo de medida y seleccione **Incluir grupo de medidas como**. Elija **Crear** o **Modificar**y envíe la consulta a una ventana. El identificador del grupo de medida estará visible en la definición del objeto. Copie el identificador de la definición del objeto.  
  
#### <a name="step-2-run-the-query"></a>Paso 2: ejecutar la consulta  
  
1.  En [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], haga clic con el botón derecho en una base de datos, señale **Nueva consulta**y seleccione **XMLA**.  
  
2.  Copie el ejemplo de código siguiente en la ventana de consulta XMLA. Cambio `DatabaseID` al identificador de la base de datos en la conexión actual.  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID> Adventure Works DW Multidimensional</DatabaseID>  
      </Object>  
    </ClearCache>  
  
    ```  
  
     También puede especificar una ruta de acceso de un objeto secundario, como un grupo de medida, para borrar la memoria caché solo para ese objeto.  
  
    ```  
    <ClearCache xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
      <Object>  
        <DatabaseID>Adventure Works DW Multidimensional</DatabaseID>  
            <CubeID>Adventure Works</CubeID>  
            <MeasureGroupID>Fact Currency Rate</MeasureGroupID>  
      </Object>  
    </ClearCache>  
    ```  
  
3.  Presione F5 para ejecutar la consulta. Debe ver el siguiente resultado:  
  
    ```  
    <return xmlns="urn:schemas-microsoft-com:xml-analysis">  
      <root xmlns="urn:schemas-microsoft-com:xml-analysis:empty" />  
    </return>  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Secuencia de comandos de las tareas administrativas en Analysis Services](../script-administrative-tasks-in-analysis-services.md)   
 [Supervisión de una instancia de Analysis Services](monitor-an-analysis-services-instance.md)  
  
  