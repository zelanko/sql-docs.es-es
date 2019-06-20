---
title: Suplantación (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: fcc79e96-182a-45e9-8ae2-aeb440e9bedd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81e8f9ae90db3c7613ccb99039d70d9a28c5a113
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067058"
---
# <a name="impersonation-ssas-tabular"></a>Suplantación (SSAS tabular)
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
  
 Es importante comprender cómo se especifican y protegen las credenciales de suplantación, así como la diferencia entre los contextos en los que ambos actual ha iniciado en credenciales del usuario y cuando se usan otras credenciales.  
  
 **Descripción de las credenciales del servidor**  
  
 En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], las credenciales para cada origen de datos se especifican mediante la página **Información de suplantación** del Asistente para la importación de tablas o modificando una conexión de origen de datos existente en el cuadro de diálogo **Conexiones existentes** .  
  
 Cuando se importan o procesan los datos, las credenciales especificadas en la página **Información de suplantación** se usan para conectarse al origen de datos y capturar los datos. Se trata de una operación *del servidor* que se ejecuta en el contexto de una aplicación cliente porque el servidor de Analysis Services que hospeda la base de datos del área de trabajo se conecta al origen de datos y captura los datos.  
  
 Al implementar un modelo en un servidor de Analysis Services, si la base de datos del área de trabajo está en la memoria cuando se implementa el modelo, las credenciales se pasan al servidor de Analysis Services en el que se implementa el modelo. Las credenciales de usuario no se almacenan en el disco en ningún momento.  
  
 Cuando un modelo implementado procesa los datos de un origen de datos, las credenciales de suplantación, almacenadas en la base de datos en memoria, se usan para conectarse al origen de datos y capturar los datos. Dado que este proceso lo controla el servidor de Analysis Services que administra la base de datos del modelo, esta también es una operación de servidor.  
  
 **Descripción de las credenciales del lado cliente**  
  
 Al crear un nuevo modelo o al agregar un origen de datos a un modelo existente, se usa el Asistente para la importación de tablas para conectarse a un origen de datos y seleccionar las tablas y vistas que se van a importar en el modelo. En el Asistente para la importación de tablas, en la página **Seleccionar tablas y vistas** , puede usar la característica **Vista previa y aplicar filtro** para ver una muestra (limitada a 50 filas) de los datos que se van a importar. También puede especificar filtros para excluir los datos que no es necesario incluir en el modelo.  
  
 De forma similar, para los modelos que ya se han creado, puede usar el cuadro de diálogo **Editar propiedades de tabla** para obtener una vista previa y filtrar los datos importados en una tabla. Estas funciones de vista previa y filtrado emplean la misma funcionalidad que la característica **Vista previa y filtrar** de la página **Seleccionar tablas y vistas** del Asistente para la importación de tablas.  
  
 La característica **Vista previa y aplicar filtro** y los cuadros de diálogo **Propiedades de tabla** y **Administrador de partición** son operaciones del *lado cliente* en proceso (es decir, lo que se realiza durante estas operaciones es diferente de cómo se ha conectado con el origen de datos y cómo se capturan los datos desde el origen de datos, que son operaciones del lado servidor). Las credenciales utilizadas para obtener una vista previa y filtrar los datos son las credenciales del usuario que ha iniciado sesión actualmente. Operaciones del lado cliente siempre utilizan credenciales de Windows del usuario actual para conectarse al origen de datos.  
  
 Esta separación entre las credenciales usadas durante las operaciones de lado servidor y las del lado cliente puede dar lugar a un error de coincidencia entre lo que ve el usuario con la característica **Vista previa y aplicar filtro** o el cuadro de diálogo **Propiedades de tabla** (operaciones del lado cliente) y los datos que se capturarán durante una importación o un procesamiento (una operación del lado servidor). Si las credenciales del usuario que ha iniciado sesión actualmente y las credenciales de suplantación especificadas son diferentes, los datos que se ven en la característica **Vista previa y filtrar** o en el cuadro de diálogo **Propiedades de tabla** y los datos capturados durante una importación o un procesamiento pueden ser diferentes según las credenciales que requiera el origen de datos.  
  
> [!IMPORTANT]  
>  Al crear un modelo, asegúrese de que las credenciales del usuario que ha iniciado sesión actualmente y las credenciales especificadas para la suplantación tienen derechos suficientes para capturar los datos del origen de datos.  
  
##  <a name="bkmk_imp_info_options"></a> Opciones  
 Al configurar la suplantación, o al modificar las propiedades de una conexión de origen de datos existente en Analysis Services, puede especificar una de las opciones siguientes:  
  
|Opción|ImpersonationMode<sup>1</sup>|Descripción|  
|------------|-----------------------------------|-----------------|  
|**Nombre de usuario de Windows específico y la contraseña** <sup>2</sup>|ImpersonateWindowsUserAccount|Esta opción especifica que el modelo usa una cuenta de usuario de Windows para importar o procesar datos del origen de datos. El dominio y el nombre de la cuenta de usuario tienen el siguiente formato: **\<nombre de dominio >\\< nombre de la cuenta de usuario\>** . Esta es la opción predeterminada al crear un modelo nuevo mediante el Asistente para la importación de tablas.|  
|**Cuenta de servicio**|ImpersonateServiceAccount|Esta opción especifica que el modelo usa las credenciales de seguridad asociadas a la instancia de servicio de Analysis Services que administra el modelo.|  
  
 <sup>1</sup>ImpersonationMode especifica el valor de la [elemento DataSourceImpersonationInfo &#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl) propiedad del origen de datos.  
  
 <sup>2</sup>cuando se usa esta opción, si se quita la base de datos del área de trabajo de la memoria, ya sea debido a un reinicio o el **retención de área de trabajo** propiedad está establecida en **descargar de la memoria** o  **Eliminar área de trabajo**, y el proyecto de modelos está cerrado, en la sesión posterior, si intenta procesar los datos de tabla, se le pedirá que escriba las credenciales para cada origen de datos. De forma similar, si una base de datos de modelo implementada se quita de la memoria, se le pedirán las credenciales para cada origen de datos.  
  
##  <a name="bkmk_impers_sec"></a> Seguridad  
 Las credenciales utilizadas con la suplantación las almacena en memoria el motor analítico en memoria xVelocity (VertiPaq)™ asociado al servidor de Analysis Services que administra la base de datos del área de trabajo o un modelo implementado.  Las credenciales no se almacenan en el disco en ningún momento. Si la base de datos del área de trabajo no está en la memoria cuando se implementa el modelo, se pedirá al usuario que escriba las credenciales necesarias para conectarse al origen de datos y capturar los datos.  
  
> [!NOTE]  
>  Se recomienda especificar una cuenta de usuario y una contraseña de Windows para las credenciales de suplantación. Una cuenta de usuario de Windows se puede configurar para que use los privilegios mínimos necesarios para conectarse al origen de datos y leer datos del mismo.  
  
##  <a name="bkmk_imp_newmodel"></a> Suplantación al importar un modelo  
 A diferencia de los modelos tabulares, que pueden usar varios modos de suplantación para admitir la recopilación de datos fuera de proceso, PowerPivot usa un solo modo: ImpersonateCurrentUser. Dado que PowerPivot siempre se ejecuta en proceso, se conecta a orígenes de datos mediante las credenciales del usuario que ha iniciado sesión actualmente. Con los modelos tabulares, las credenciales del usuario que ha iniciado sesión actualmente solo se usan con la característica **Vista previa y filtrar** del Asistente para la importación de tablas y cuando se ven las **Propiedades de tabla**. Las credenciales de suplantación se usan al importar o procesar datos en la base de datos del área de trabajo, o al importar o procesar datos en un modelo implementado.  
  
 Al crear un modelo nuevo importando un libro PowerPivot existente, de forma predeterminada, el diseñador de modelos configurará la suplantación para usar la cuenta de servicio (ImpersonateServiceAccount). Se recomienda cambiar las credenciales de suplantación en los modelos importados desde PowerPivot a una cuenta de usuario de Windows. Una vez importado el libro PowerPivot y creado el nuevo modelo en el Diseñador de modelos, puede cambiar las credenciales mediante el **las conexiones existentes** cuadro de diálogo.  
  
 Al crear un modelo nuevo importando desde un modelo existente en un servidor de Analysis Services, las credenciales de suplantación se pasan de la base de datos del modelo existente a la base de datos del área de trabajo del modelo nuevo. Si fuera necesario, puede cambiar las credenciales en el modelo nuevo mediante el cuadro de diálogo **Conexiones existentes** .  
  
##  <a name="bkmk_conf_imp_info"></a> Configurar la suplantación  
 El lugar y el contexto en el que existe un modelo determinarán cómo se configura la información de suplantación. Para los proyectos que se crean en el [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], puede configurar la información de suplantación en la página **Información de suplantación** del Asistente para la importación de tablas o modificando una conexión a un origen de datos en el cuadro de diálogo **Conexiones existentes** . Para ver las conexiones existentes, en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], en el menú **Modelo** , haga clic en **Conexiones existentes**.  
  
 Para los modelos que se implementan en un servidor de Analysis Services, la información de suplantación puede configurarse haciendo clic en el botón de puntos suspensivos (...) de la **información de suplantación de origen de datos** propiedad en el **depropiedadesdebasededatos** cuadro de diálogo de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Modo DirectQuery &#40;SSAS tabular&#41;](directquery-mode-ssas-tabular.md)   
 [Orígenes de datos &#40;SSAS tabular&#41;](../data-sources-ssas-tabular.md)   
 [Implementación de soluciones de modelos tabulares &#40;SSAS tabular&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
