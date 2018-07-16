---
title: Implementación de soluciones de modelos tabulares (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: aff96558-e5e5-4b95-8ddf-ee0709c842fb
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 99b9e1594c4d4fbe07a6085544021b94820db640
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220045"
---
# <a name="tabular-model-solution-deployment-ssas-tabular"></a>Implementación de soluciones de modelos tabulares (SSAS tabular)
  Después de crear un proyecto de modelo tabular, deberá implementarlo para que los usuarios examinen el modelo usando una aplicación cliente de informes. Este tema describe las diferentes propiedades y métodos que puede utilizar al implementar soluciones de modelo tabular en el entorno.  
  
 Secciones de este tema:  
  
-   [Ventajas](#bkmk_benefits)  
  
-   [Implementar un modelo tabular a partir de SQL Server Data Tools (SSDT)](#bkmk_deploying_bism)  
  
-   [Propiedades de implementación](#bkmk_deploy_props)  
  
-   [Métodos de implementación](#bkmk_meth)  
  
-   [Configurar el servidor de implementación y conectarse con un modelo implementado](#bkmk_connecting)  
  
-   [Tareas relacionadas](#bkmk_rt)  
  
##  <a name="bkmk_benefits"></a> Ventajas  
 Al implementar un modelo tabular se crea una base de datos del modelo en un entorno de pruebas, ensayo o producción. Los usuarios pueden conectarse al modelo implementado mediante un archivo de conexión .bism en Sharepoint o mediante una conexión de datos directamente desde las aplicaciones cliente de informes, como Microsoft Excel, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], o una aplicación personalizada. La base de datos del área de trabajo del modelo, que se genera al crear un proyecto de modelo tabular en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y se usa para crear el modelo, permanecerá en la instancia del servidor del área de trabajo, lo que permite realizar cambios en el proyecto de modelo y volver a implementarlo después en el entorno de pruebas, ensayo o producción cuando sea necesario.  
  
##  <a name="bkmk_deploying_bism"></a> Implementar un modelo tabular a partir de SQL Server Data Tools (SSDT)  
 La implementación es un proceso sencillo; sin embargo, se deben realizar algunos pasos para asegurarse de que el modelo se implementa en la instancia adecuada de Analysis Services y con las opciones de configuración correctas.  
  
 Los modelos tabulares se definen con varias propiedades de implementación específicas. Durante la implementación, se establece una conexión con la instancia de Analysis Services especificada en la propiedad **Servidor** . A continuación, se crea en esa instancia una nueva base de datos modelo con el nombre especificado en la propiedad **Database** , si no existe ninguna. Los metadatos del archivo Model.bim del proyecto de modelo se usan para configurar los objetos de la base de datos del modelo en el servidor de implementación. La **Opción de procesamiento**le permite especificar si solo se implementan los metadatos del modelo, si se crea la base de datos del modelo o, si se especifica **Predeterminado** o **Completo** , las credenciales de suplantación usadas para conectarse con orígenes de datos se pasan "en memoria" de la base de datos del área de trabajo del modelo a la base de datos implementada del modelo. A continuación, Analysis Services ejecuta el procesamiento para rellenar los datos en el modelo implementado. Una vez completado el proceso de implementación, las aplicaciones cliente pueden conectarse con el modelo mediante una conexión de datos o mediante un archivo de conexión .bism en SharePoint.  
  
##  <a name="bkmk_deploy_props"></a> Propiedades de implementación  
 Las propiedades Opciones de implementación y Servidor de implementación del proyecto especifican el modo y el lugar en el que se implementa un modelo en un entorno de Analysis Services de ensayo o de producción. Aunque la configuración de las propiedades predeterminadas se define para todos los proyectos de modelo, puede cambiar estas opciones de las propiedades para cada proyecto en función de los requisitos de implementación específicos. Para más información sobre cómo configurar las propiedades de implementación predeterminadas, vea [Configurar las propiedades predeterminadas de modelado de datos y de implementación &#40;SSAS Tabular&#41;](properties-ssas-tabular.md).  
  
### <a name="deployment-options-properties"></a>Propiedades de las opciones de implementación  
 Entre las propiedades de las opciones de implementación se incluyen:  
  
|Property|Valor predeterminado|Descripción|  
|--------------|---------------------|-----------------|  
|**Opción de procesamiento**|**Default**|Esta propiedad especifica el tipo de procesamiento necesario cuando se implementan cambios en los objetos. Esta propiedad tiene las opciones siguientes:<br /><br /> **Valor predeterminado** : este valor especifica que Analysis Services determinará el tipo de procesamiento necesario. Los objetos sin procesar se procesarán y, si fuera necesario, se volverán a calcular las relaciones de atributo, las jerarquías de atributo, las jerarquías de usuario y las columnas calculadas. Esta configuración produce como resultado un menor tiempo de implementación que la opción de procesamiento completo.<br /><br /> **No Procesar** : este valor especifica que solamente se implementarán los metadatos. Después de la implementación, puede que sea necesario ejecutar una operación de procesamiento en el modelo implementado para actualizar y recalcular los datos.<br /><br /> **Completo** : este valor especifica que los metadatos están implementados y que se realiza una operación Proceso completo. Esto garantiza que el modelo implementado tiene las actualizaciones más recientes de los metadatos y los datos.|  
|**Implementación transaccional**|**False**|Esta propiedad especifica si la implementación es o no transaccional. De manera predeterminada, la implementación de todos los objetos modificados no es transaccional con el procesamiento de dichos objetos implementados. La implementación puede ser correcta y persistir aunque se produzca un error de procesamiento. Puede cambiar este comportamiento para incluir la implementación y el procesamiento en una sola transacción.|  
|**Modo de consulta**|**In-Memory**|Esta propiedad especifica el modo en que se ejecuta el origen cuyos resultados de la consulta se devuelven: modo In-Memory (almacenamiento en caché) o modo de DirectQuery. Esta propiedad tiene las opciones siguientes:<br /><br /> **DirectQuery** : este valor especifica que todas las consultas del modelo deben utilizar solo el origen de datos relacional.<br /><br /> **DirectQuery con In-Memory** : este valor especifica que, de forma predeterminada, las consultas se deben responder con el origen relacional, a menos que se especifique lo contrario en la cadena de conexión desde el cliente.<br /><br /> **In-Memory** : este valor especifica que las consultas tienen que responderse únicamente con la caché.<br /><br /> **In-Memory con DirectQuery** : este valor especifica, de forma predeterminada, que las consultas se deben responder mediante caché, a menos que se especifique lo contrario en la cadena de conexión de cliente.<br /><br /> <br /><br /> Para más información, vea [Modo DirectQuery &#40;SSAS tabular&#41;](directquery-mode-ssas-tabular.md).|  
  
### <a name="deployment-server-properties"></a>Propiedades del servidor de implementación  
 Entre las propiedades del servidor de implementación se incluyen:  
  
|Property|Valor predeterminado|Descripción|  
|--------------|---------------------|-----------------|  
|**Servidor**<br /><br /> Establézcalo cuando se cree el proyecto.|**localhost**|Esta propiedad, establecida cuando se crea el proyecto, especifica el nombre de la instancia de Analysis Services en la que se implementará el modelo. De forma predeterminada, el modelo se implementará en la instancia predeterminada de Analysis Services del equipo local. Sin embargo, puede cambiar este valor para especificar una instancia con nombre en el equipo local o cualquier instancia en cualquier equipo remoto en el que tenga permiso para crear objetos de Analysis Services.|  
|**Edición**|La misma edición que la instancia en la que se encuentra el servidor del área de trabajo.|Esta propiedad especifica la edición del servidor de Analysis Services en la que se implementará el modelo. La edición del servidor define varias características que se pueden incorporar al proyecto. De forma predeterminada, la edición será la del servidor de Analysis Services local. Si especifica otro servidor de Analysis Services, por ejemplo, uno de producción, asegúrese de especificar la edición de ese servidor de Analysis Services.|  
|**Base de datos**|**\<ProjectName >**|Esta propiedad especifica el nombre de la base de datos de Analysis Services en la que se crearán instancias de los objetos de modelo durante la implementación. Este nombre también se especificará en una conexión de datos del cliente de informes o en un archivo de conexión de datos .bism.<br /><br /> Puede cambiar este nombre en cualquier momento durante la creación del modelo. Si cambia el nombre después de haber implementado el modelo, los cambios realizados no afectarán al modelo implementado previamente. Por ejemplo, si abre una solución denominada `TestDB` e implementar su solución con el nombre de base de datos de modelo predeterminado modelo y, a continuación, modifica la solución y cambia el nombre de la base de datos de modelo `Sales`, la instancia de Analysis Services se implementaron las soluciones a le mostrar separar las bases de datos, una denominada modelo y otra denominada Sales.|  
|**Nombre del cubo**|**Modelo**|Esta propiedad especifica el nombre del cubo como se muestra en las herramientas cliente (por ejemplo, Excel) y en AMO (Objetos de administración de análisis).|  
  
### <a name="directquery-options-properties"></a>Propiedades de las opciones de DirectQuery  
 Entre las propiedades de las opciones de implementación se incluyen:  
  
|Property|Valor predeterminado|Descripción|  
|--------------|---------------------|-----------------|  
|**Configuración de suplantación**|**Predeterminado**|Esta propiedad especifica la configuración de suplantación que se usa cuando un modelo que se ejecuta en el modo DirectQuery se conecta con los orígenes de datos. Las credenciales de suplantación no se usan al consultar la memoria caché en memoria. El valor de esta propiedad tiene las opciones siguientes:<br /><br /> **Predeterminado** : este valor especifica que Analysis Services usará la opción que se especificó en la página Información de suplantación cuando se creó la conexión con el origen de datos mediante el Asistente para la importación de tablas.<br /><br /> **ImpersonateCurrentUser** : este valor especifica que la cuenta del usuario que ha iniciado sesión actualmente se usará para conectarse con todos los orígenes de datos.|  
  
##  <a name="bkmk_meth"></a> Métodos de implementación  
 Puede utilizar varios métodos para implementar un proyecto de modelos tabulares. La mayoría de los métodos de implementación que se pueden utilizar para otros proyectos de Analysis Services, como multidimensional, también se pueden utilizar para implementar proyectos de modelos tabulares.  
  
|Método|Descripción|Vínculo|  
|------------|-----------------|----------|  
|**Implementar el comando en Herramientas de datos de SQL Server**|El comando Implementar proporciona un método sencillo e intuitivo para implementar un proyecto de modelos tabulares del entorno de creación de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] .<br /><br /> **\*\* Precaución \*\*** Este método no se debe usar para implementar servidores de producción. Con este método, puede sobrescribir ciertas propiedades de un modelo existente.|[Implementar desde SQL Server Data Tools &#40;Tabular de SSAS&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|  
|**Automatización AMO (Objetos de administración de análisis)**|AMO ofrece una interfaz programática para el conjunto de comandos completo establecido para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], incluidos los comandos que se pueden usar para la implementación de soluciones. Como método para la implementación de soluciones, la automatización AMO es el más flexible, pero también requiere un esfuerzo de programación.  Una ventaja clave de AMO es que puede usar el Agente SQL Server con la aplicación AMO para ejecutar la implementación siguiendo una programación preestablecida.|[Desarrollar con objetos de administración de análisis &#40;AMO&#41;](../multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)|  
|**XMLA**|Use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para generar un script XMLA de los metadatos de una base de datos existente de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, a continuación, ejecute el script en otro servidor para volver a crear la base de datos inicial. Los scripts XMLA se forman fácilmente en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] definiendo el proceso de implementación, codificándolo y guardándolo en un script XMLA. Una vez que se tiene un script XMLA en un archivo guardado, se puede ejecutar fácilmente de acuerdo con una programación, o bien se puede incrustar en una aplicación que se conecta directamente con una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].<br /><br /> También se pueden ejecutar Scripts XMLA de forma preestablecida con el Agente SQL Server, pero este método no presenta la misma flexibilidad que AMO. AMO ofrece una mayor funcionalidad, al hospedar todo el espectro de comandos administrativos.|[Implementar soluciones de modelo mediante XMLA](../multidimensional-models/deploy-model-solutions-using-xmla.md)|  
|**Asistente para la implementación**|Use el Asistente para la implementación cuando desee usar los archivos de salida XMLA generados por un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implementar los metadatos del proyecto en un servidor de destino. Con el Asistente para la implementación, puede implementar directamente desde el archivo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , tal como lo creó el directorio de salida en la compilación del proyecto.<br /><br /> La principal ventaja de usar el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es la comodidad. Al igual que se puede guardar un script XMLA para su uso posterior en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], se pueden guardar los scripts del Asistente para la implementación. El Asistente para la implementación se puede ejecutar interactivamente y desde el símbolo del sistema mediante la utilidad de implementación.|[Implementar soluciones con el Asistente para la implementación](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|  
|**Utilidad de implementación**|La utilidad de implementación le permite iniciar el motor de implementación de Analysis Services desde un símbolo del sistema.|[Implementar soluciones de modelos con la utilidad de implementación](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|  
|**Asistente para sincronizar bases de datos**|Use el Asistente para sincronizar bases de datos cuando desee sincronizar los metadatos y los datos de dos bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cualquiera.<br /><br /> El Asistente para sincronizar se puede usar para copiar datos y metadatos de un servidor de origen en un servidor de destino. Si el servidor de destino no tiene una copia de la base de datos que desea implementar, se copia una nueva base de datos en el servidor de destino. Si el servidor de destino ya tiene una copia de la misma base de datos, la base de datos del servidor de destino se actualiza para que use los metadatos y los datos de la base de datos de origen.|[Sincronizar bases de datos de Analysis Services](../multidimensional-models/synchronize-analysis-services-databases.md)|  
|**Copias de seguridad y restauración**|La copia de seguridad es la forma más simple de transferir bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Desde el cuadro de diálogo **Copia de seguridad** , puede establecer la configuración de las opciones y, a continuación, puede ejecutar la copia de seguridad desde el mismo cuadro de diálogo. O bien, puede crear un script que se puede guardar y ejecutar con la frecuencia necesaria.<br /><br /> Las copias de seguridad y restauración no se usan con la misma frecuencia que los otros métodos de implementación, pero es una forma de completar rápidamente una implementación con requisitos mínimos de infraestructura.|[Realizar una copia de seguridad y restaurar las bases de datos de Analysis Services](../multidimensional-models/backup-and-restore-of-analysis-services-databases.md)|  
  
##  <a name="bkmk_connecting"></a> Configurar el servidor de implementación y conectarse con un modelo implementado  
 Una vez implementado un modelo, hay consideraciones adicionales para proteger el acceso a los datos del modelo, las copias de seguridad y las operaciones de procesamiento que pueden configurarse en el servidor de Analysis Services usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Aunque estas propiedades y opciones de configuración están fuera del ámbito de este tema, sin embargo son muy importantes para garantizar que los datos del modelo implementado están seguros, se mantienen actualizados y constituyen un valioso recurso de análisis de datos para los usuarios de la organización.  
  
 Una vez implementado un modelo y configuradas las opciones del servidor, se puede conectar con el modelo desde las aplicaciones cliente de informes y usarlo para examinar y analizar sus metadatos. La conexión con una base de datos de modelo implementada desde aplicaciones cliente está fuera del ámbito de este tema. Para obtener más información sobre la conexión con una base de datos del modelo desde aplicaciones cliente, vea [Tabular Model Data Access](tabular-model-data-access.md).  
  
##  <a name="bkmk_rt"></a> Tareas relacionadas  
  
|Tarea|Descripción|  
|----------|-----------------|  
|[Implementar desde SQL Server Data Tools &#40;Tabular de SSAS&#41;](deploy-from-sql-server-data-tools-ssas-tabular.md)|Describe cómo configurar las propiedades de implementación e implementar un proyecto de modelo tabular mediante el comando Implementar en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].|  
|[Implementar soluciones con el Asistente para la implementación](../multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)|En los temas de esta sección se describe cómo usar el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implementar soluciones de modelo tabular y multidimensional.|  
|[Implementar soluciones de modelos con la utilidad de implementación](../multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|Describe cómo usar la utilidad de implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para implementar soluciones de modelo tabular y multidimensional.|  
|[Implementar soluciones de modelo mediante XMLA](../multidimensional-models/deploy-model-solutions-using-xmla.md)|Describe cómo usar XMLA para implementar las soluciones tabulares y multidimensionales de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Sincronizar bases de datos de Analysis Services](../multidimensional-models/synchronize-analysis-services-databases.md)|Describe cómo usar el Asistente para sincronizar bases de datos con el fin de sincronizar los metadatos y los datos entre dos bases de datos tabulares o multidimensionales de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a una base de datos de modelo Tabular &#40;SSAS&#41;](connect-to-a-tabular-model-database-ssas.md)  
  
  
