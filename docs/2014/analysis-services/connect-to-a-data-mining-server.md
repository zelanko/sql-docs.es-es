---
title: Conectarse a un servidor de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
- getting started
ms.assetid: 85962ad6-d840-4bc6-905e-c667c3276944
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3c9abd1b891d47f1711db21eec017ec755526e02
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087346"
---
# <a name="connect-to-a-data-mining-server"></a>Conectar con un servidor de minería de datos
  ![Botón conexiones](media/misc-connection.gif "botón conexiones")  
  
 Haga clic en el **conexión** botón para seleccionar una conexión existente o crear una nueva conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **¿Por qué es necesario para conectarse a un servidor?**  
  
 La creación de una conexión le permite usar los algoritmos de minería de datos que proporciona el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], así como aprovechar las ventajas del procesamiento optimizado del servidor.  
  
 No es necesario conservar los datos o los resultados en una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o de SQL Server. Los Complementos de minería de datos de Excel solo pueden trabajar con datos almacenados en Excel, o con datos con los que se conecta como un origen de datos de Excel.  
  
## <a name="how-to-create-a-new-connection"></a>Cómo crear una conexión nueva  
  
1.  Haga clic en el **conexión** botón.  
  
2.  En el **conexiones de Analysis Services** cuadro de diálogo, haga clic en **New**.  
  
3.  En el **conectar a Analysis Services** diálogo cuadro, escriba un nombre de servidor.  
  
4.  Especifique el método de autenticación.  
  
5.  Especifique el catálogo o la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] donde almacenará los modelos de minería de datos.  
  
    > [!NOTE]  
    >  Si todavía no ha creado ninguna base de datos, puede usar (predeterminado) para crear y probar la conexión; sin embargo, no es posible agregar modelos de minería de datos a la conexión predeterminada. Antes de crear cualquier modelo de minería de datos, debe crear una conexión a una base de datos existente.  
  
6.  Si se conecta al servidor a través de un servicio web, escriba el nombre de usuario y la contraseña requeridos por dicho servicio web.  
  
7.  Escriba un nombre descriptivo para la nueva conexión.  
  
8.  Haga clic en **Probar conexión** para comprobar que el servidor está disponible.  
  
## <a name="troubleshooting-connections"></a>Solucionar problemas de las conexiones  
 Esta sección proporciona respuestas a algunas preguntas comunes sobre conexiones con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Obtengo un mensaje que dice "Se encontró ninguna conexión."**  
  
 Si el texto de la parte inferior del botón indica **sin conexión**, significa que no ha creado una conexión a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos, o error de la conexión. Es posible seguir trabajando en Excel con datos de Access u otros orígenes, pero, para crear un modelo de minería de datos o ejecutar una consulta de predicción, es necesario disponer de una conexión activa.  
  
 **¿Supongamos que no tiene permiso para usar el servidor?**  
  
 Si no dispone de los permisos necesarios para almacenar los modelos de minería de datos en el servidor, o si desea probar la minería de datos sin guardar el trabajo, puede utilizar las Herramientas de análisis de tabla, que crean estructuras de datos y modelos temporales. Todavía necesita poder almacenar modelos temporales en el servidor. Pida al administrador para habilitar el uso de *modelos de minería de datos de sesión* en el servidor.  
  
 Si desea asegurarse de que los modelos se guardan, puede deshabilitar la opción para utilizar modelos temporales o puede usar los asistentes del Cliente de minería de datos. Estos asistentes almacenan todos los modelos en el servidor. Necesitará acceso administrativo a la base de datos donde se almacenan los modelos, por lo que se recomienda solicitar al administrador la creación de una base de datos especial para crear modelos de minería de datos con los complementos.  
  
 **Se perdió la conexión; ¿perdí todo mi trabajo?**  
  
 Si termina la conexión con el servidor, los resultados y los datos no se perderán, ya que se almacenan en Excel. Sin embargo, si ha creado algunos modelos temporales, estos se eliminarán del servidor después de un breve período de tiempo. Por lo que si pierde la conexión temporalmente, en algún momento los modelos no se eliminará todavía.  
  
 Los datos o los resultados generados no se perderán, ya que todos los informes y las tablas se almacenan en Excel.  
  
> [!NOTE]  
>  No se desconecte del servidor ni de la red mientras el complemento se esté comunicando con el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Por ejemplo, no se desconecte nunca mientras se esté creando un modelo o mientras se estén procesando los datos. En algunas situaciones, los datos podrían resultar dañados.  
  
 **No puedo conectarme al modelo mediante las herramientas de Visio**  
  
 Las Plantillas de minería de datos para Visio no pueden usar modelos ni estructuras de minería de datos temporales. Para crear un diagrama de un modelo de minería de datos, éste debe estar almacenado en un servidor.  
  
 **¿Cómo se puede supervisar el uso de la conexión?**  
  
 El [seguimiento &#40;cliente de minería de datos para Excel&#41; ](trace-data-mining-client-for-excel.md) herramienta crea un registro de todas las actividades entre los complementos y el servidor especificado.  
  
 Para habilitar la supervisión de modelos de sesión, seleccione la **usar modelos de sesión** opción el **seguimiento** cuadro de diálogo.  
  
 El seguimiento le permite ver los comandos DMX y XMLA que se generan mientras se crean modelos y estructuras. También puede ver las consultas enviadas por el cliente para generar resultados e informes en Excel.  
  
 **¿Qué es un modelo temporal? ¿Cómo puedo guardar un modelo temporal?**  
  
 Las Herramientas de análisis de tabla para Excel crean estructuras de datos y modelos de minería de datos temporales de forma predeterminada. Puede continuar examinando y consultando modelos temporales siempre y cuando mantenga el libro abierto y no se desconecte de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 En cuanto cierre el libro de Excel o cambie o finalice la conexión con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], se eliminarán todas las estructuras y modelos de sesión que haya creado.  
  
 Cuando se completa un asistente en el Cliente de minería de datos para Excel, los modelos se guardan en el servidor de forma predeterminada, pero en la última página de cada asistente hay una opción que permite usar un modelo temporal. Si selecciona esta opción, tanto el modelo como la estructura de minería de datos que ha creado se almacenarán en un archivo temporal. Puede examinar, administrar y modificar la estructura y el modelo mientras Excel permanezca abierto. Sin embargo, cuando cierre Excel, se eliminarán la estructura y los modelos relacionados.  
  
 Puede crear explícitamente un modelo o estructura temporal mediante el **Editor minería de datos avanzada consulta** y seleccionando una de las plantillas DMX. Agregue la cláusula `USE SESSION MODELS` para especificar que los objetos deben ser temporales.   
  
### <a name="creating-backups-of-mining-models-and-structures"></a>Crear copias de seguridad de modelos y estructuras de minería de datos  
 Para crear una copia de seguridad de un modelo o estructura, puede exportarlo mediante el uso de [administrar modelos &#40;complementos de minería de datos de SQL Server&#41;](manage-models-sql-server-data-mining-add-ins.md), en el cliente de minería de datos para Excel.  
  
 Si creó un modelo de minería de datos temporal, este normalmente tendrá un nombre que resulta difícil de entender, por ejemplo Table5_593679_TS_62446. Sin embargo, puede usar el [seguimiento &#40;cliente de minería de datos para Excel&#41; ](trace-data-mining-client-for-excel.md) herramienta para detectar los nombres de las estructuras temporales y los modelos creados por las herramientas de análisis de tabla y, a continuación, realizar copias de seguridad mediante  **Administrar modelos**.  
  
##### <a name="identify-and-export-a-temporary-model"></a>Identificar y exportar un modelo temporal  
  
1.  En el **conexiones** grupo del cliente de minería de datos para Excel, haga clic en **seguimiento**.  
  
2.  Vea el registro de actividad de conexión y busque el modelo revisando las columnas y las salidas de predicción (por ejemplo).  
  
     Usuarios avanzados: Si está familiarizado con DMX o XMLA, puede copiar las instrucciones en un archivo para su uso posterior.  
  
3.  Cuando haya encontrado el nombre del modelo temporal y de estructura, abrir **Administrar modelo** y seleccione el modelo.  
  
4.  Haga clic en Exportar este modelo de minería de datos para generar un archivo de script en la ubicación que especifique.  
  
## <a name="see-also"></a>Vea también  
 [Conectarse a datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md)   
 [Utilidad de configuración del servidor &#40;datos complementos de minería de datos para Excel&#41;](server-configuration-utility-data-mining-add-ins-for-excel.md)  
  
  
