---
title: Propiedades de los modelos | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bd9cb6ffd5eed5a1f066fa66056f15041296f738
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="model-properties"></a>Propiedades del modelo 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Este artículo describen las propiedades del modelo. Cada proyecto de modelos tabulares tiene propiedades del modelo que afectan al modo en que se compila el modelo que se está creando con las herramientas de desarrollo de SQL Server, cómo se realizan las copias de seguridad y cómo se almacena la base de datos del área de trabajo. Las propiedades del modelo que se describen aquí no se aplican a los modelos que se han implementado previamente.  
  
 Secciones de este tema:  
  
-   [Propiedades de modelo](#bkmk_model_properties)  
  
-   [Configurar los valores de las propiedades del modelo](#bkmk_conf_model_prop)  
  
##  <a name="bkmk_model_properties"></a> Propiedades del modelo  
 **Avanzadas**  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|**Acción de compilación**|Compilar|Esta propiedad especifica el modo en que el archivo está relacionado con el proceso de compilación e implementación. El valor de esta propiedad tiene las opciones siguientes:<br /><br /> **Compilar** : se produce una acción de compilación normal. Las definiciones de los objetos del modelo se escribirán en el archivo .asdatabase.<br /><br /> **Ninguna** : la salida al archivo .asdatabase estará vacía.|  
|**Copiar en el directorio de salida**|No copiar|Esta propiedad especifica que el archivo de origen se copiará en el directorio de salida. El valor de esta propiedad tiene las opciones siguientes:<br /><br /> **No copiar** : no se crea ninguna copia en el directorio de salida.<br /><br /> **Copiar siempre** : siempre se crea una copia en el directorio de salida.<br /><br /> **Copiar si es posterior** : se crea una copia en el directorio de salida solo si hay cambios en el archivo model.bim.|  
  
 **Varios**  
  
> [!NOTE]  
>  Algunas propiedades se establecen automáticamente cuando se crea el modelo y no se pueden cambiar.  
  
> [!NOTE]  
>  Las propiedades Servidor del área de trabajo, Retención del área de trabajo y Copia de seguridad de datos tienen valores predeterminados que se aplican al crear un nuevo proyecto de modelo. Puede cambiar la configuración predeterminada para los modelos nuevos en la página Modelado de datos en la configuración de Analysis Server del cuadro de diálogo Herramientas\Opciones. Estas propiedades, al igual que otras, también se pueden establecer para cada modelo en la ventana Propiedades. Para obtener más información, consulte [configurar las propiedades de implementación y de modelado de datos predeterminadas](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md).  
  
|Propiedad|Valor predeterminado|Description|  
|--------------|---------------------|-----------------|  
|**Intercalación**|Intercalación predeterminada para el equipo en el que está instalado Visual Studio.|El designador de intercalación del modelo.|  
|**Nivel de compatibilidad**|Valor predeterminado u otro seleccionado al crear el proyecto.|Se aplica a SQL Server 2012 Analysis Services SP1 o posterior. Especifica las características y los valores disponibles para este modelo. Para obtener más información, vea [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).|  
|**Copia de seguridad de datos**|No hacer copia de seguridad en disco|Especifica si se mantiene una copia de seguridad de los datos del modelo en un archivo de copia de seguridad. El valor de esta propiedad tiene las opciones siguientes:<br /><br /> **Hacer copia de seguridad en disco** : especifica que se debe mantener una copia de seguridad de los datos del modelo en el disco. Cuando se guarda el modelo, los datos también se guardarán en el archivo de copia de seguridad (ABF). La selección de esta opción puede hacer que se alarguen los tiempos empleados para cargar y guardar modelos.<br /><br /> **No hacer copia de seguridad en disco** : especifica que no se debe mantener una copia de seguridad de los datos del modelo en el disco. Esta opción minimizará el tiempo necesario para guardar y cargar el modelo.<br /><br /> <br /><br /> La configuración predeterminada para esta propiedad se puede cambiar en la página Modelado de datos en la configuración de Analysis Server del cuadro de diálogo Herramientas\Opciones.| 
|**Dirección del filtro predeterminado**|En una sola dirección|Determina la dirección del filtro predeterminado para nuevas relaciones.| 
|**Modo DirectQuery**|Desactivado|Especifica si este modelo funciona en modo DirectQuery. Para obtener más información, consulte [Directquerymode](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md).|  
|**Nombre de archivo**|Model.bim|Especifica el nombre del archivo .bim. El nombre del archivo no se debe cambiar.|  
|**Ruta de acceso completa**|Ruta de acceso que se especificó cuando se creó el proyecto.|La ubicación del archivo model.bim. Esta propiedad no se puede establecer en la ventana Propiedades.|  
|**Idioma**|Inglés|El idioma predeterminado del modelo. El idioma predeterminado se determina mediante el idioma de Visual Studio. Esta propiedad no se puede establecer en la ventana Propiedades.|  
|**Base de datos del área de trabajo**|El nombre del proyecto, seguido de un subrayado y de un GUID.|El nombre de la base de datos del área de trabajo usada para almacenar y modificar en la memoria el modelo correspondiente al archivo model.bim seleccionado. Esta base de datos aparecerá en la instancia de Analysis Services especificada en la propiedad Servidor del área de trabajo. Esta propiedad no se puede establecer en la ventana Propiedades. Para obtener más información, consulte [base de datos del área de trabajo](../../analysis-services/tabular-models/workspace-database-ssas-tabular.md).|  
|**Retención de área de trabajo**|Descargar de la memoria|Especifica cómo se conserva una base de datos del área de trabajo después de que se cierre un modelo. Una base de datos del área de trabajo incluye los metadatos del modelo, los datos importados en un modelo y las credenciales de suplantación (cifradas). En algunos casos, la base de datos del área de trabajo puede ser muy grande y usar una cantidad significativa de memoria. De forma predeterminada, las bases de datos del área de trabajo se descargan de la memoria. Al cambiar este valor, es importante tener en cuenta los recursos de memoria disponibles así como la frecuencia con que se piensa trabajar en el modelo. El valor de esta propiedad tiene las opciones siguientes:<br /><br /> **Mantener en memoria** : especifica que, después de cerrar un modelo, la base de datos del área de trabajo se debe mantener en la memoria. Esta opción usará más memoria; sin embargo, al abrir un modelo, se usan menos recursos y la base de datos del área de trabajo se cargará más rápido.<br /><br /> **Descargar de la memoria** : especifica que, después de cerrar un modelo, la base de datos del área de trabajo se debe mantener en el disco, pero no en la memoria. Esta opción usa menos memoria; sin embargo, al abrir un modelo, se usan recursos adicionales y el modelo se cargará más lentamente que cuando la base de datos del área de trabajo se mantiene en la memoria. Use esta opción cuando los recursos de memoria sean limitados o cuando trabaje en una base de datos de área de trabajo remota.<br /><br /> **Eliminar área de trabajo** : especifica que la base de datos del área de trabajo se debe eliminar de la memoria y que no se debe mantener en el disco después de que se cierre el modelo. Esta opción usa menos memoria y espacio de almacenamiento; sin embargo, al abrir un modelo, se usan recursos adicionales y el modelo se cargará más lentamente que cuando la base de datos del área de trabajo se mantiene en la memoria o en el disco. Use esta opción cuando solo trabaje ocasionalmente con modelos.<br /><br /> <br /><br /> La configuración predeterminada para esta propiedad se puede cambiar en la página Modelado de datos en la configuración de Analysis Server del cuadro de diálogo Herramientas\Opciones.|  
|**Servidor del área de trabajo**|localhost|Esta propiedad especifica el servidor predeterminado que se usará para hospedar la base de datos del área de trabajo mientras se crea el modelo. Todas las instancias disponibles de Analysis Services que se ejecutan en el equipo local se incluyen en el cuadro de lista.<br /><br /> La configuración predeterminada para esta propiedad se puede cambiar en la página Modelado de datos en la configuración de Analysis Server del cuadro de diálogo Herramientas\Opciones.<br /><br /> <br /><br /> Nota: Se recomienda especificar siempre un servidor de Analysis Services local como servidor del área de trabajo. Para las bases de datos del área de trabajo de un servidor remoto, la importación desde [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no se admite, no se pueden realizar copias de seguridad de los datos localmente y la interfaz de usuario puede experimentar latencia durante las consultas.|  
  
##  <a name="bkmk_conf_model_prop"></a> Configurar los valores de las propiedades del modelo  
  
1.  En SSDT, en el **Explorador de soluciones**, haga clic en el archivo **Model.bim** .  
  
2.  En la ventana **Propiedades** , haga clic en una propiedad y, a continuación, escriba un valor o haga clic en la flecha abajo para seleccionar una opción de configuración.  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades de implementación y de modelado de datos predeterminadas](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Propiedades de proyecto](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)  
  
  
