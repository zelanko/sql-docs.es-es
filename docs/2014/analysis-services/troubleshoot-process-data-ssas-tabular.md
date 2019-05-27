---
title: Solución de problemas de procesamiento de datos (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 678f523c-e181-4456-9a54-7b7bf044b8d2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f76d67d5e44fc700d4b889840ef2dcc07a0bfde0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065766"
---
# <a name="troubleshoot-process-data-ssas-tabular"></a>Solucionar problemas del procesamiento de datos (SSAS tabular)
  Este tema incluye información sobre el procesamiento (actualización) de los datos de un modelo cuando este se crea con [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]; no incluye información sobre el procesamiento de datos de modelos implementados en una instancia de servidor de Analysis Services. Para obtener más información sobre el procesamiento de los datos de un modelo implementado, vea [Crear scripts para tareas administrativas en Analysis Services](script-administrative-tasks-in-analysis-services.md).  
  
 Secciones de este tema:  
  
-   [Cómo funciona el procesamiento de datos](#bkmk_how_df_works)  
  
-   [Efectos del procesamiento de datos](#bkmk_impact_of_df)  
  
-   [Determinar el origen de datos](#bkmk_det_source)  
  
-   [Determinar cuándo se actualizaron los datos por última vez](#bkmk_det_last_ref)  
  
-   [Restricciones en los orígenes de datos actualizables](#bkmk_restrictions)  
  
-   [Restricciones en los cambios de un origen de datos](#bkmk_rest_changes)  
  
##  <a name="bkmk_how_df_works"></a> Cómo funciona el procesamiento de datos  
 Cuando se procesan datos, los datos del Diseñador de modelos se reemplazan por los nuevos datos. No se pueden importar únicamente las filas de datos que son nuevas, o solo los datos que han cambiado, ya que el Diseñador de modelos no realiza un seguimiento de las filas que se agregaron anteriormente.  
  
 El procesamiento de datos funciona como una transacción. Esto significa que, una vez iniciada la actualización de datos, esta debe completarse o no efectuarse; nunca tendrá datos que sean parcialmente correctos.  
  
 El procesamiento manual de datos, que se inicia desde la ventana de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], se administra mediante la instancia en memoria local de Analysis Services. Por consiguiente, la operación de procesamiento de datos puede afectar al rendimiento de otras tareas del equipo. Sin embargo, si programa el procesamiento automático de datos en un modelo implementado mediante un script, la instancia de Analysis Services administrará el proceso de importación y el momento en que se realiza.  
  
##  <a name="bkmk_impact_of_df"></a> Efectos del procesamiento de datos  
 El procesamiento de datos suele desencadenar el nuevo cálculo de estos.  Procesar los datos significa obtener los datos más recientes de los orígenes externos; recalcular significa actualizar el resultado de todas las fórmulas que usan datos que han cambiado. Una operación de procesamiento normalmente conlleva otra de recálculo.  
  
 Por lo tanto, antes de modificar los orígenes de datos o de procesar los datos que se obtienen del origen de datos, siempre hay que tener en cuenta los posibles efectos y consecuencias:  
  
-   Algunas partes de los datos del modelo pueden dejar de funcionar como consecuencia de los cambios realizados en el origen de datos. Si no se pueden recuperar todas las columnas del origen de datos (por ejemplo, si se han eliminado o han cambiado), se producirá un error en el procesamiento y deberá actualizar las asignaciones entre el origen de datos y los datos del modelo. Para obtener más información, vea [Editar una conexión de origen de datos existente &#40;SSAS tabular&#41;](edit-an-existing-data-source-connection-ssas-tabular.md);  
  
-   Después del procesamiento, algunas columnas podrían aparecer marcadas para indicar que contienen un error. Esto puede ocurrir porque la fórmula DAX de la columna usa datos que dejaron de estar disponibles durante el procesamiento, porque el tipo de datos de una columna cambió, o porque se agregó un valor no válido a los datos externos. Para resolver el problema, puede editar la fórmula o eliminar la columna si está basada en datos que ya no están disponibles.  
  
-   Las fórmulas que usan los datos actualizados se tendrán que volver a calcular. Dependiendo del tamaño del modelo, esta tarea puede llevar bastante tiempo.  
  
-   Si el modelo contiene varios orígenes de datos, puede que tenga que procesarlo completamente (Procesar todo), aunque solo haya cambiado un origen de datos externo. Por ejemplo, si crea medidas que dependen de columnas calculadas y dichas columnas calculadas usan valores de otras columnas calculadas, el Diseñador de modelos analizará primero las dependencias y, a continuación, procesará toda la cadena de objetos relacionados en orden. Dependiendo de la complejidad de las dependencias, esta tarea puede llevar mucho tiempo.  
  
-   Cuando se cambia un filtro, es necesario recalcular el modelo completo.  
  
##  <a name="bkmk_det_source"></a> Determinar el origen de datos  
 Si no está seguro de la procedencia de los datos de un modelo, puede usar las herramientas de la ventana de [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para obtener los detalles, incluido el nombre y la ruta de acceso del archivo de origen.  
  
#### <a name="to-find-the-source-of-existing-data"></a>Para encontrar el origen de datos existentes  
  
1.  En el Diseñador de modelos, seleccione la tabla que contiene los datos cuyo origen desea conocer.  
  
2.  Haga clic en el menú **Tabla** y, a continuación, en **Propiedades de la tabla**.  
  
3.  En el cuadro de diálogo **Editar propiedades de tabla** , anote el valor indicado en **Nombre de conexión**.  
  
4.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Conexiones existentes**.  
  
5.  En el cuadro de diálogo **Conexiones existentes** , seleccione el origen de datos con el nombre que encontró en el paso 3, y haga clic en **Editar**.  
  
6.  En el cuadro de diálogo **Editar conexiones** , consulte la información de conexión, como el nombre de la base de datos, ruta de acceso del archivo o ruta de acceso del informe.  
  
##  <a name="bkmk_det_last_ref"></a> Determinar cuándo se actualizaron los datos por última vez  
 Use las propiedades de la tabla para determinar cuándo se actualizaron los datos por última vez.  
  
#### <a name="to-find-the-date-and-time-that-a-table-was-last-processed"></a>Para conocer la fecha y hora en que se procesó una tabla por última vez  
  
1.  En el Diseñador de modelos, seleccione la tabla que contiene los datos cuya fecha de actualización desea conocer.  
  
2.  Haga clic en el menú **Tabla** y, a continuación, en **Propiedades de la tabla**.  
  
3.  En el cuadro de diálogo **Editar propiedades de tabla** , **Última actualización** muestra la última fecha en que se actualizó la tabla.  
  
##  <a name="bkmk_restrictions"></a> Restricciones en los orígenes de datos actualizables  
 Algunas restricciones se aplican a los orígenes de datos que se pueden procesar de forma automática desde un modelo implementado en una instancia de Analysis Services. Asegúrese de seleccionar solo los orígenes de datos que cumplan los siguientes criterios:  
  
-   El origen de datos debe estar disponible en la ubicación indicada en el momento en que se produce el procesamiento de datos. Si el origen de datos original está en una unidad de disco local del usuario que creó el modelo, debe excluir ese origen de datos de la operación de procesamiento de datos o encontrar una manera de publicar ese origen de datos en una ubicación que sea accesible a través de una conexión de red. Si mueve un origen de datos a una ubicación de red, asegúrese de abrir el modelo en el Diseñador de modelos y repita los pasos de recuperación de datos. Esto es necesario para restablecer la información de conexión que está almacenada en las propiedades de conexión del origen de datos.  
  
-   Se debe obtener acceso al origen de datos usando las credenciales que están incrustadas en la conexión de origen de datos. Las credenciales incrustadas se crean en la conexión de origen de datos al conectar con el origen de datos externo.  
  
-   El procesamiento de datos debe realizarse para todos los orígenes de datos que especifique. De lo contrario, se descartan los datos procesados y se conserva únicamente la última versión guardada del modelo. Excluya cualquier origen de datos en el que no confíe completamente.  
  
-   El procesamiento de datos no debe invalidar otros datos del modelo. Al procesar un subconjunto de los datos, es importante que sepa si el modelo sigue siendo válido después de haber agregado nuevos datos con datos estáticos que no pertenecen al mismo período. Como diseñador de modelos, depende de usted conocer las dependencias de sus datos y asegurarse de que el procesamiento de estos es adecuado para el propio modelo.  
  
     A un origen de datos externo se tiene acceso a través de una cadena de conexión incrustada, una dirección URL o una ruta UNC que se especifica al importar los datos originales en el modelo usando el Asistente para la importación de tablas. La información de conexión original que está almacenada en la conexión de origen de datos se vuelve a usar para las siguientes operaciones de actualización de los datos. No hay ninguna información de conexión independiente que se cree y se administre con fines de procesamiento de datos; solo se usa la información de conexión existente.  
  
##  <a name="bkmk_rest_changes"></a> Restricciones en los cambios de un origen de datos  
 Hay algunas restricciones en los cambios que se pueden realizar en un origen de datos:  
  
-   Los tipos de datos de una columna solo se pueden cambiar a un tipo de datos compatible. Por ejemplo, si los datos de la columna contienen números decimales, el tipo de datos no se puede cambiar a un entero. Sin embargo, los datos numéricos se pueden cambiar a texto. Para obtener más información sobre los tipos de datos, vea [Tipos de datos compatibles &#40;SSAS tabular&#41;](tabular-models/data-types-supported-ssas-tabular.md).  
  
-   No se pueden seleccionar varias columnas de distintas tablas y cambiar las propiedades de las columnas. Solo se puede trabajar con tablas o vistas de una en una.  
  
## <a name="see-also"></a>Vea también  
 [Procesar manualmente los datos &#40;SSAS tabular&#41;](manually-process-data-ssas-tabular.md)   
 [Editar una conexión de origen de datos existente &#40;SSAS tabular&#41;](edit-an-existing-data-source-connection-ssas-tabular.md)  
  
  
