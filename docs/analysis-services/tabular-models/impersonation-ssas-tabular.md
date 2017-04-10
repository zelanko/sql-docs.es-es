---
title: "Suplantaci&#243;n (SSAS tabular) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
caps.latest.revision: 20
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 20
---
# Suplantaci&#243;n (SSAS tabular)
  Este tema proporciona a los autores de modelos tabulares una descripción de cómo usa Analysis Services las credenciales de inicio de sesión al conectarse a un origen de datos para importar y procesar (actualizar) datos.  
  
 Este artículo contiene las secciones siguientes:  
  
-   [Ventajas](#bkmk_how_imper)  
  
-   [Opciones](#bkmk_imp_info_options)  
  
-   [Seguridad](#bkmk_impers_sec)  
  
-   [Suplantación al importar un modelo](#bkmk_imp_newmodel)  
  
-   [Configurar la suplantación](#bkmk_conf_imp_info)  
  
##  <a name="bkmk_how_imper"></a> Ventajas  
 La*suplantación* es la capacidad de una aplicación de servidor, como Analysis Services, de asumir la identidad de una aplicación cliente. Analysis Services se ejecuta con una cuenta de servicio; sin embargo, cuando el servidor establece conexión con un origen de datos, usa la suplantación, de modo que puedan realizarse las comprobaciones de acceso para la importación y el procesamiento de datos.  
  
 Las credenciales usadas para la suplantación son diferentes de las credenciales del usuario que ha iniciado sesión actualmente. Las credenciales del usuario que tiene abierta una sesión se usan para determinadas operaciones del lado cliente mientras se crea un modelo.  
  
 Es importante entender cómo se especifican y protegen las credenciales de suplantación, así como la diferencia entre los contextos en los que se usan tanto las credenciales del usuario que tiene abierta una sesión como las demás credenciales.  
  
 **Descripción de las credenciales del servidor**  
  
 En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], las credenciales para cada origen de datos se especifican mediante la página **Información de suplantación** del Asistente para la importación de tablas o modificando una conexión de origen de datos existente en el cuadro de diálogo **Conexiones existentes** .  
  
 Cuando se importan o procesan los datos, las credenciales especificadas en la página **Información de suplantación** se usan para conectarse al origen de datos y capturar los datos. Se trata de una operación *del servidor* que se ejecuta en el contexto de una aplicación cliente porque el servidor de Analysis Services que hospeda la base de datos del área de trabajo se conecta al origen de datos y captura los datos.  
  
 Al implementar un modelo en un servidor de Analysis Services, si la base de datos del área de trabajo está en la memoria cuando se implementa el modelo, las credenciales se pasan al servidor de Analysis Services en el que se implementa el modelo. Las credenciales de usuario no se almacenan en el disco en ningún momento.  
  
 Cuando un modelo implementado procesa los datos de un origen de datos, las credenciales de suplantación, almacenadas en la base de datos en memoria, se usan para conectarse al origen de datos y capturar los datos. Dado que este proceso lo controla el servidor de Analysis Services que administra la base de datos del modelo, esta también es una operación de servidor.  
  
 **Descripción de las credenciales del lado cliente**  
  
 Al crear un nuevo modelo o al agregar un origen de datos a un modelo existente, se usa el Asistente para la importación de tablas para conectarse a un origen de datos y seleccionar las tablas y vistas que se van a importar en el modelo. En el Asistente para la importación de tablas, en la página **Seleccionar tablas y vistas**, puede usar la característica **Vista previa y aplicar filtro** para ver una muestra (limitada a 50 filas) de los datos que se van a importar. También puede especificar filtros para excluir los datos que no es necesario incluir en el modelo.  
  
 De forma similar, para los modelos que ya se han creado, puede usar el cuadro de diálogo **Editar propiedades de tabla** para obtener una vista previa y filtrar los datos importados en una tabla. Estas funciones de vista previa y filtrado emplean la misma funcionalidad que la característica **Vista previa y filtrar** de la página **Seleccionar tablas y vistas** del Asistente para la importación de tablas.  
  
 La característica **Vista previa y aplicar filtro** y los cuadros de diálogo **Propiedades de tabla** y **Administrador de partición** son operaciones del *lado cliente* en proceso (es decir, lo que se realiza durante estas operaciones es diferente de cómo se ha conectado con el origen de datos y cómo se capturan los datos desde el origen de datos, que son operaciones del lado servidor). Las credenciales utilizadas para obtener una vista previa y filtrar los datos son las credenciales del usuario que ha iniciado sesión actualmente. Las operaciones del lado cliente siempre utilizan las credenciales de Windows del usuario actual para conectarse al origen de datos.  
  
 Esta separación entre las credenciales usadas durante las operaciones de lado servidor y las del lado cliente puede dar lugar a un error de coincidencia entre lo que ve el usuario con la característica **Vista previa y aplicar filtro** o el cuadro de diálogo **Propiedades de tabla** (operaciones del lado cliente) y los datos que se capturarán durante una importación o un procesamiento (una operación del lado servidor). Si las credenciales del usuario que ha iniciado sesión actualmente y las credenciales de suplantación especificadas son diferentes, los datos que se ven en la característica **Vista previa y filtrar** o en el cuadro de diálogo **Propiedades de tabla** y los datos capturados durante una importación o un procesamiento pueden ser diferentes según las credenciales que requiera el origen de datos.  
  
> [!IMPORTANT]  
>  Al crear un modelo, asegúrese de que las credenciales del usuario que ha iniciado sesión actualmente y las credenciales especificadas para la suplantación tienen derechos suficientes para capturar los datos del origen de datos.  
  
##  <a name="bkmk_imp_info_options"></a> Opciones  
 Al configurar la suplantación, o al modificar las propiedades de una conexión de origen de datos existente en Analysis Services, puede especificar una de las opciones siguientes:  
  
|Opción|ImpersonationMode*|Description|  
|------------|-------------------------|-----------------|  
|**Nombre de usuario y contraseña específicos de Windows***\*|ImpersonateWindowsUserAccount|Esta opción especifica que el modelo usa una cuenta de usuario de Windows para importar o procesar datos del origen de datos. El dominio y el nombre de la cuenta de usuario tienen el formato siguiente: **\<nombre de dominio>\\<nombre de cuenta de usuario\>**. Esta es la opción predeterminada al crear un modelo nuevo mediante el Asistente para la importación de tablas.|  
|**Cuenta de servicio**|ImpersonateServiceAccount|Esta opción especifica que el modelo usa las credenciales de seguridad asociadas a la instancia de servicio de Analysis Services que administra el modelo.|  
  
 * ImpersonationMode especifica el valor de la propiedad del [Elemento DataSourceImpersonationInfo &#40;ASSL&#41;](../../analysis-services/scripting/properties/datasourceimpersonationinfo-element-assl.md) en el origen de datos.  
  
 \*\*Cuando se usa esta opción, si la base de datos del área de trabajo se quita de la memoria (debido a un reinicio o a que la propiedad **Retención de área de trabajo** está establecida en **Descargar de la memoria** o en **Eliminar del área de trabajo** y el proyecto de modelos se cierra), si intenta procesar los datos de la tabla en la siguiente sesión, se le pedirá que especifique las credenciales para cada origen de datos. De forma similar, si una base de datos de modelo implementada se quita de la memoria, se le pedirán las credenciales para cada origen de datos.  
  
##  <a name="bkmk_impers_sec"></a> Seguridad  
 Las credenciales utilizadas con la suplantación las almacena en memoria el motor analítico en memoria xVelocity (VertiPaq)™ asociado al servidor de Analysis Services que administra la base de datos del área de trabajo o un modelo implementado.  Las credenciales no se almacenan en el disco en ningún momento. Si la base de datos del área de trabajo no está en la memoria cuando se implementa el modelo, se pedirá al usuario que escriba las credenciales necesarias para conectarse al origen de datos y capturar los datos.  
  
> [!NOTE]  
>  Se recomienda especificar una cuenta de usuario y una contraseña de Windows para las credenciales de suplantación. Una cuenta de usuario de Windows se puede configurar para que use los privilegios mínimos necesarios para conectarse al origen de datos y leer datos del mismo.  
  
##  <a name="bkmk_imp_newmodel"></a> Suplantación al importar un modelo  
 A diferencia de los modelos tabulares, que pueden usar varios modos de suplantación para admitir la recopilación de datos fuera de proceso, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] usa un solo modo; ImpersonateCurrentUser. Como [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] siempre se ejecuta en proceso, se conecta a orígenes de datos con las credenciales del usuario que actualmente ha iniciado la sesión. Con los modelos tabulares, las credenciales del usuario que ha iniciado sesión actualmente solo se usan con la característica **Vista previa y filtrar** del Asistente para la importación de tablas y cuando se ven las **Propiedades de tabla**. Las credenciales de suplantación se usan al importar o procesar datos en la base de datos del área de trabajo, o al importar o procesar datos en un modelo implementado.  
  
 Cuando se crea un modelo a través de la importación de un libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] existente, de forma predeterminada, el diseñador de modelos configurará la suplantación para usar la cuenta de servicio (ImpersonateServiceAccount). Se recomienda cambiar las credenciales de suplantación en los modelos importados desde [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a una cuenta de usuario de Windows. Una vez que se importa el libro [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] y se crea el nuevo modelo en el diseñador de modelos, puede cambiar las credenciales mediante el cuadro de diálogo **Conexiones existentes** .  
  
 Al crear un modelo nuevo importando desde un modelo existente en un servidor de Analysis Services, las credenciales de suplantación se pasan de la base de datos del modelo existente a la base de datos del área de trabajo del modelo nuevo. Si fuera necesario, puede cambiar las credenciales en el modelo nuevo mediante el cuadro de diálogo **Conexiones existentes** .  
  
##  <a name="bkmk_conf_imp_info"></a> Configurar la suplantación  
 El lugar y el contexto en el que existe un modelo determinarán cómo se configura la información de suplantación. Para los proyectos que se crean en el [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], puede configurar la información de suplantación en la página **Información de suplantación** del Asistente para la importación de tablas o modificando una conexión a un origen de datos en el cuadro de diálogo **Conexiones existentes** . Para ver las conexiones existentes, en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Conexiones existentes**.  
  
 Para los modelos que se implementan en un servidor de Analysis Services, la información de suplantación se puede configurar en SSMS, en **Propiedades de conexión** > **Información de suplantación**.  
  
## Vea también  
 [Modo DirectQuery &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)   
 [Orígenes de datos &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/data-sources-ssas-tabular.md)   
 [Implementación de soluciones de modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md)  
  
  