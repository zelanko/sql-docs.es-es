---
title: Actualizar Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
caps.latest.revision: 79
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 3b3ad4ecf62f3a30882720140f2f362007f8428b
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="upgrade-analysis-services"></a>Actualizar Analysis Services
  Es posible actualizar las instancias de Analysis Services a una versión de SQL Server del mismo modo de servidor con el objetivo de aprovechar las características que incorpora la nueva versión, tal y como se describe en [What's New in Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md) (Novedades de Analysis Services).  
  
 Puede actualizar cada instancia de forma local, por separado de otras instancias que se ejecuten en el mismo hardware. Sin embargo, la mayoría de los administradores optan por instalar una nueva instancia de la versión más reciente para efectuar pruebas con aplicaciones antes de transferir las cargas de trabajo de producción al nuevo servidor. Pero, en el caso de los servidores de entornos de desarrollo o pruebas, una actualización local puede resultar más práctica.  
  
 Antes de actualizarse a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], revise lo siguiente:  

- En [Notas de la versión de SQL Server 2017](../../sql-server/sql-server-2017-release-notes.md) se describen los problemas conocidos y las soluciones alternativas.  
- En[SQL Server 2016 Release Notes](../../sql-server/sql-server-2016-release-notes.md) (Notas de la versión de SQL Server 2016) se describen los problemas conocidos y las soluciones alternativas.  
- En[Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md) se resumen las características descontinuadas, en desuso y modificadas. Debe revisar estas listas periódicamente para evaluar el impacto que podrían tener los cambios de nuestros productos en sus modelos, scripts o código personalizado. Normalmente, las transiciones de características se anuncian con la versión preliminar de la siguiente versión principal.  
  
## <a name="server-upgrade"></a>Actualización de servidores  
 Existen dos enfoques básicos para actualizar servidores y bases de datos:  
  
-   Las**actualizaciones locales** reemplazan los archivos de programa existentes por los de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Las bases de datos permanecen en la misma ubicación. Las carpetas de programas se actualizan para reflejar el nuevo nombre.  
  
-   Las**actualizaciones en paralelo** crean una nueva instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]; por lo general, en el mismo equipo, a menos que también cambie de hardware al mismo tiempo. Para aplicar este enfoque, tendrá que migrar las bases de datos a la nueva instancia y, después, desinstalar la versión anterior si desea liberar espacio en disco.  
  
 Los niveles de compatibilidad de las bases de datos asociadas a un servidor determinado seguirán siendo los mismos, a menos que los cambie manualmente.  
  
### <a name="in-place-upgrade"></a>Actualización en contexto  
 Puede actualizar una instancia existente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, como parte del proceso de actualización, migrar automáticamente las bases de datos existentes de la antigua instancia a la nueva. Dado que los metadatos y los datos binarios son compatibles entre las dos versiones, después de actualizar se conservarán los datos y no es necesario migrarlos manualmente.  
  
 Para actualizar una instancia existente, ejecute el programa de instalación y especifique el nombre de la instancia existente como nombre de la nueva instancia.  
  
### <a name="side-by-side-upgrade"></a>Actualización en paralelo  
  
-   Realice copias de seguridad de todas las bases de datos y compruebe que se puedan restaurar. Consulte [Backup and Restore of Analysis Services Databases](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md).  
  
-   Identifique un subconjunto de informes, hojas de cálculo o instantáneas del panel a fin de utilizarlo más adelante como base para confirmar las operaciones del servidor posteriores a la actualización. Si fuera posible, recopile medidas de rendimiento para que pueda llevar a cabo comparaciones utilizando las mismas cargas de trabajo en un servidor actualizado.  
  
-   Instale una nueva instancia de Analysis Services; para ello, elija el mismo modo de servidor (tabular o multidimensional) que tenga la instancia que pretende reemplazar. Consulte [Install Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md).  
  
     Realice las tareas posteriores a la instalación para configurar los puertos y agregar los administradores del servidor. Vea [Configuración posterior a la instalación &#40;Analysis Services&#41;](../../analysis-services/instances/post-install-configuration-analysis-services.md).  
  
-   Adjunte o restaure cada base de datos.  
  
-   Ejecute DBCC para comprobar la integridad de las bases de datos. Los modelos tabulares se someten a una comprobación más completa, en la que se incluyen pruebas de objetos huérfanos en toda la jerarquía del modelo. En lo que respecta a los modelos multidimensionales, solo se comprueban los índices de partición. Vea [Comprobador de coherencia de base de datos &#40;DBCC&#41; para bases de datos multidimensionales y tabulares de Analysis Services](../../analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services.md).  
  
-   Pruebe los informes, las hojas de cálculo y los paneles para confirmar que no haya ningún cambio adverso en el comportamiento o los cálculos. Debería observar un funcionamiento más rápido tanto para cargas de trabajo multidimensionales como para las tabulares.  
  
-   Pruebe las operaciones de procesamiento y corrija cualquier problema de inicio de sesión o permisos. Si utiliza la cuenta de servicio predeterminada para las conexiones, el nuevo servicio se ejecuta en una cuenta diferente. Para obtener más información sobre las cuentas de inicio de Analysis Services, vea [Configurar las cuentas de servicio &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md).  
  
-   Pruebe las operaciones de copia de seguridad y restauración en el servidor actualizado ajustando los scripts para que utilicen el nuevo nombre del servidor.  
  
## <a name="database-upgrade"></a>Actualización de bases de datos  
 Las bases de datos creadas en versiones anteriores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se ejecutan en el servidor actualizado con la configuración de nivel de compatibilidad de base de datos más antigua. Por lo general, es posible actualizar una base de datos o un modelo para que funcionen con un nivel de compatibilidad superior a fin de disfrutar de nuevas características, pero tenga presente que, si opta por hacerlo, quedará vinculado a una versión específica del servidor.  
  
 Para actualizar una base de datos, normalmente se actualiza el modelo en SQL Server Data Tools (SSDT) y, después, se implementa la solución en una instancia del servidor actualizada. Consulte [Descarga de SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) para obtener la versión más reciente.  
  
 Las bases de datos tabulares y multidimensionales siguen rutas de versión distintas. Es una coincidencia que los modelos multidimensionales y tabulares tengan un nivel de compatibilidad 1100.  Los modos avanzarán a ritmos distintos si los cambios de características solo repercuten en uno de ellos.  
  
 Para ofrecer un poco de contexto, en la siguiente tabla se resumen los niveles de compatibilidad. Sin embargo, debe revisar los temas detallados para comprender qué ofrece cada nivel.  
  
||||  
|-|-|-|  
|Tabular|1200|SQL Server 2016|  
|Tabular|1103|SQL Server 2014|  
|Tabular|1100|SQL Server 2012|  
|Multidimensional|1100|SQL Server 2012 y posterior|  
|Multidimensional|1050|SQL Server 2005, 2008 y 2008 R2|  
  
 Para obtener más información, vea [Nivel de compatibilidad de una base de datos multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md) y [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).  
  
## <a name="tabular-model-upgrade-to-1200-compatibility-level"></a>Actualización del modelo tabular al nivel de compatibilidad 1200  
 Las bases de datos y los modelos tabulares son los que más ventajas obtienen de SQL Server 2016. En esta versión, se ofrece un modo DirectQuery revisado para modelos tabulares con el nivel de compatibilidad 1200, que se simplifica gracias a la eliminación del modo híbrido, la adición de instrucciones de consulta para recuperar un subconjunto de datos en tiempo de diseño, así como seguridad de nivel de fila mediante DAX, en lugar de permisos de filas en la base de datos back-end.  
  
 Un segundo motivo para actualizar radica en la nueva construcción de metadatos tabulares dentro del modelo. Un modelo tabular con el nuevo nivel de compatibilidad 1200, con independencia de que se cree con este último o se actualice a él, utiliza terminología nativa para las definiciones de objetos, como modelo, tabla, relaciones y columnas, a fin de describir sus elementos principales.  
  
 Para actualizar un modelo tabular, use una versión de [SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx) creada para esta versión a fin de cambiar el valor de la propiedad **Nivel de compatibilidad** a **SQL Server 2016 RTM (1200)**.  
  
 No utilice SSMS, fragmentos de código o scripts para cambiar **CompatibilityLevel**. Por sí mismo, el cambio de propiedad carece de efecto alguno. La conversión de los metadatos tiene lugar en SSDT como respuesta a la actualización de la propiedad, tras lo cual se vuelve a abrir el proyecto.  
  
 Como siempre, asegúrese de guardar una copia de seguridad del modelo antes de efectuar la actualización, por si tuviera que revertir a la versión previa a la actualización.  
  
1.  En SSDT > Explorador de soluciones, haga clic con el botón derecho en **model.bim**, elija **Ver código** y confirme que el modelo se cerrará y se volverá a abrir en una nueva ventana (la ventana de código).  
  
2.  El modelo se abrirá como un documento XMLA. Para poder efectuar una comparación después de la conversión, copie el contenido en otro archivo (puede abrir uno nuevo con formato XML en SSDT).  
  
3.  Haga clic con el botón derecho en **model.bim** y vuelva a cambiarlo a **Diseñador de vistas**.  
  
4.  Establezca **Nivel de compatibilidad** en  **SQL Server 2016 RTM (1200)**.  
  
5.  Este paso no puede revertirse, por lo que se le pedirá que confirme la acción. Haga clic en **Sí** para continuar. Se actualizará el proyecto.  
  
6.  Haga clic con el botón derecho en **model.bim** y vuelva a cambiarlo a **Ver código**.  
  
     Observe que la definición del modelo es ahora JSON y que se utilizan metadatos tabulares.  
  
 **Conversión de metadatos**  
  
 Si compara los metadatos de antes y después de la conversión, observará que se convierten en JSON y se eliminan sus definiciones redundantes.  
  
 El modelo conserva todas la funcionalidad: los enlaces de datos, los segmentos de particiones, las expresiones, los identificadores de objetos, los nombres de objetos, las descripciones, los títulos, las traducciones y las anotaciones permanecerán intactos. Pero si tiene algún fragmento de código o script que haga referencia a objetos específicos, parte de la reescritura del código incluirá la eliminación de las referencias a objetos que ya no existan. Por ejemplo, un modelo de 1050 o 1103 tendrá secciones para dimensiones externas al cubo, mientras que en un modelo de 1200 se define una tabla como un único objeto.  
  
> [!NOTE]  
>  Los niveles de compatibilidad tabulares más antiguos, de 1050 y 1103, son compatibles, pero se encuentran en desuso. En alguna versión futura de SQL Server, dejarán de admitirse los modelos tabulares convertidos en objetos multidimensionales. Consulte [Deprecated Analysis Services Features in SQL Server 2016](../../analysis-services/deprecated-analysis-services-features-in-sql-server-2016.md) para ver el anuncio.  
  
## <a name="post-upgrade-for-tabular-models-at-1200-compatibilitylevel"></a>Procedimientos posteriores a la actualización para modelos tabulares con un nivel de compatibilidad 1200  
 Una vez que se haya convertido el modelo, deberá usar [Tabular Model Scripting Language &#40;TMSL&#41; Reference](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md) (Referencia de lenguaje de scripting del modelo tabular) en lugar de XMLA para crear scripts con las operaciones de la base de datos. TMSL se genera automáticamente en SSMS cuando el modelo es de 1200. Los fragmentos de código personalizados que tengan como objetivo bases de datos tabulares de 1200 deben utilizar la API definida en el espacio de nombres Microsoft.AnalysisServices.Tabular. Los fragmentos de código y los scripts se deberán escribir desde cero; no hay ningún mecanismo para realizar una conversión integrada. Vea [Guía del desarrollador (Analysis Services)](../../analysis-services/analysis-services-developer-documentation.md) para obtener más información.  
  
 También puede agregar las siguientes características a un modelo tabular, que solo es compatible con el nivel de compatibilidad 1200:  
  
-   Una implementación de DirectQuery que admite ahora seguridad de nivel de fila mediante DAX en el modelo, más orígenes de datos, subconjuntos de datos para fines de modelado y una configuración más simple.  
  
-   Columnas calculadas  
  
-   Carpetas para mostrar  
  
## <a name="upgrade-tabular-models-in-directquery-mode"></a>Actualización de los modelos tabulares en el modo DirectQuery  
 No puede realizar una actualización local de modelos tabulares más antiguos configurados para DirectQuery. La nueva implementación de DirectQuery presenta un menor número de opciones de configuración, por lo que no se pueden portar todos los ajustes.  
  
1.  En SSDT, desactive el modo **DirectQuery** para que el modelo use el almacenamiento en memoria. Consulte [Habilitar el modo de diseño de DirectQuery (SSAS Tabular)](https://msdn.microsoft.com/library/hh270245.aspx) para obtener instrucciones.  
  
2.  Establezca **Nivel de compatibilidad** en SQL Server 2016 (RTM) 1200.  
  
3.  Guarde y recompile o implemente el modelo.  
  
4.  Vuelva a activar **DirectQuery** . Consulte [DirectQuery for Tabular 1200 models](http://msdn.microsoft.com/library/4227977e-7368-4d45-b78f-24076882e7a8) para obtener más instrucciones.  
  
## <a name="see-also"></a>Vea también  
 [Modo DirectQuery &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Novedades de Analysis Services](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)   
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Actualización de PowerPivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Instalar Analysis Services en el modo de minería de datos y multidimensional](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Actualización a SQL Server 2016 mediante el Asistente para instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  

