---
title: Importar valores de un proyecto de limpieza en un dominio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.kb.importprojectvalues.f1
ms.assetid: f23e38e2-39e0-42d7-abd5-34d8fcca5d2a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4239776908aaca1f6f925baa6ce412dcc71bc343
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51032362"
---
# <a name="import-cleansing-project-values-into-a-domain"></a>Importar valores de un proyecto de limpieza en un dominio
  En [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS), puede importar el conocimiento de calidad de los datos durante el proceso de limpieza en un proyecto de limpieza de calidad de datos o un paquete de Integration Services que contenga el componente Limpieza de DQS en un dominio. De este modo, se garantiza la conservación del conocimiento de confianza y la continua mejora de la base de conocimiento.  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
  
-   Para importar los valores del proyecto de limpieza en un dominio, el dominio debe haberse utilizado en el proyecto de limpieza en Data Quality Cliente o en el paquete de Integration Services que contiene un componente de Limpieza de DQS.  
  
-   El proyecto de limpieza de Data Quality Client o el paquete de Integration Services que contiene el componente de Limpieza de DQS deben haberse completado correctamente.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN para importar en un dominio el conocimiento de calidad de datos obtenido durante el proceso de limpieza.  
  
##  <a name="Import"></a> Importar valores de proyecto de limpieza  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra una base de conocimiento en la actividad Administración de dominios.  
  
3.  Si va a agregar valores a un dominio existente, selecciónelo en la lista de dominios.  
  
4.  Haga clic en la pestaña **Valores del dominio** , haga clic en el icono **Importar valores** de la barra de iconos y, a continuación, haga clic en **Importar valores de proyecto**. El cuadro de diálogo **Configuración de proyecto de importación** mostrará una lista de los proyectos de calidad de los datos y paquetes de Integration Services que fueron limpiados en el dominio.  
  
    > [!NOTE]  
    >  Si no se ha creado ningún proyecto utilizando el dominio o alguno de sus dominios vinculados, o el proyecto no se ha finalizado, la opción **Importar valores de proyecto** no estará disponible.  
  
5.  En el cuadro de diálogo **Configuración de proyecto de importación** :  
  
    -   Seleccione **Todos** en la lista despegable **Importado** para mostrar todos los proyectos o **No** para mostrar solo los proyectos cuyos valores no se han importado todavía.  
  
    -   Seleccione el proyecto del que desee importar los valores.  
  
    -   Seleccione **Agregar valores de la pestaña Nuevo** para importar los valores de la pestaña Nuevo, además de los valores de las pestañas **Correcto** y **Corregido** .  
  
    -   Haga clic en **Aceptar**.  
  
6.  Vuelve a la pestaña **Valores del dominio** y aparece un mensaje que indica que la importación de los valores fue correcta. Los valores que se han importado y que, por lo tanto, son nuevos en el dominio, se mostrarán en la tabla **Valores** .  
  
7.  Anule la selección de la opción **Mostrar solo nuevo** para mostrar todos los valores del dominio.  
  
8.  Seleccione **Correcto**, **Error**o **No válido** para mostrar solo los valores del tipo seleccionado.  
  
9. Para buscar una cadena específica, escríbala en el cuadro de texto **Buscar** . Haga clic en la flecha arriba o abajo para recorrer los valores que cumplen los criterios de búsqueda. Aparecerán resaltados en amarillo.  
  
10. Haga clic en **Finalizar**.  
  
    > [!NOTE]  
    >  Para obtener más información sobre cómo trabajar con valores de la pestaña **Valores del dominio** , vea [Change Domain Values](../../2014/data-quality-services/change-domain-values.md).  
  
##  <a name="FollowUp"></a> Seguimiento: después de importar valores de proyecto en un dominio  
 Una vez importado en un dominio el conocimiento de calidad de datos obtenido durante el proceso de limpieza, puede realizar otras tareas de administración de dominios en el dominio y en los valores. Para más información, vea [Administrar un dominio](../../2014/data-quality-services/managing-a-domain.md).  
  
##  <a name="Values"></a> Valores que se importarán  
 Se importarán los valores siguientes desde un proyecto a un dominio:  
  
-   Solo se importarán en el dominio los valores de cadena.  
  
-   Solamente se importarán los valores de las pestañas **Correcto**, **Corregido**y **Nuevo** de la página **Administrar y ver resultados** de la actividad **Limpieza** . Los valores de la pestaña **Nuevo** de la actividad **Limpieza** se importarán solamente si se ha activado la casilla del cuadro de diálogo **Importar valores de proyecto** .  
  
-   Los valores se importarán como correctos o como erróneos con sus correcciones. Solo se importarán los valores erróneos que tengan valores de corrección.  
  
-   El valor de corrección deberá ser un nuevo valor que no exista en la base de conocimiento o un valor correcto ya existente.  
  
-   Solo se importarán en la base de conocimiento las correcciones realizadas en el nivel de valor, no en el de registro.  
  
-   Se crearán valores no válidos si el valor importado está en contradicción con una regla de dominio.  
  
-   Si se importan valores de varios proyectos simultáneamente, la importación se realizará en orden secuencial.  
  
-   Las correcciones realizadas como resultado de una relación basada en términos de un dominio se importan como valores correctos (no como errores).  
  
##  <a name="ValuesNot"></a> Valores que no se importarán  
 No se importarán los valores siguientes desde un proyecto a un dominio:  
  
-   Los valores de las pestañas **Sugerido** y **No válido** de la página **Administrar y ver resultados** de la actividad **Limpieza** no se importarán.  
  
-   Si un valor del proyecto de limpieza está en contradicción con un valor existente en el dominio, el primer valor se omite. Esto incluirá los conflictos existentes entre los valores de la base de conocimiento y los de limpieza.  
  
-   Las correcciones realizadas en el nivel de registro no se importarán en la base de conocimiento.  
  
-   No se importará ningún valor en un dominio si el valor al que debe reemplazar lo corrigió o aprobó como correcto un servicio de datos de referencia.  
  
-   Si un valor de corrección aparece en la base de conocimiento como no válido o erróneo, no se importarán ni el error ni el valor de corrección.  
  
-   Si el dominio forma parte de un dominio compuesto y se ha realizado la limpieza en este, no se importará ningún valor.  
  
-   Solo se podrán importar valores de un proyecto si la base de conocimiento se encuentra en el estado Trabajando y la ha bloqueado el usuario que realiza la importación.  
  
## <a name="see-also"></a>Vea también  
 [Limpieza de datos](../../2014/data-quality-services/data-cleansing.md)   
 [Transformación Limpieza de DQS](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
