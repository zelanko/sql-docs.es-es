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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087346"
---
# <a name="connect-to-a-data-mining-server"></a>Conectar con un servidor de minería de datos
  ![Botón Conexiones](media/misc-connection.gif "Botón Conexiones")  
  
 Haga clic en el botón **conexión** para seleccionar una conexión existente o para crear una nueva conexión a una instancia [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]de.  
  
 **¿Por qué necesito conectarme con un servidor?**  
  
 La creación de una conexión le permite usar los algoritmos de minería de datos que proporciona el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], así como aprovechar las ventajas del procesamiento optimizado del servidor.  
  
 No es necesario conservar los datos o los resultados en una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o de SQL Server. Los Complementos de minería de datos de Excel solo pueden trabajar con datos almacenados en Excel, o con datos con los que se conecta como un origen de datos de Excel.  
  
## <a name="how-to-create-a-new-connection"></a>Cómo crear una conexión nueva  
  
1.  Haga clic en el botón **conexión** .  
  
2.  En el cuadro de diálogo **Analysis Services conexiones** , haga clic en **nuevo**.  
  
3.  En el cuadro de diálogo **conectar con Analysis Services** , escriba un nombre de servidor.  
  
4.  Especifique el método de autenticación.  
  
5.  Especifique el catálogo o la base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] donde almacenará los modelos de minería de datos.  
  
    > [!NOTE]  
    >  Si todavía no ha creado ninguna base de datos, puede usar (predeterminado) para crear y probar la conexión; sin embargo, no es posible agregar modelos de minería de datos a la conexión predeterminada. Antes de crear cualquier modelo de minería de datos, debe crear una conexión a una base de datos existente.  
  
6.  Si se conecta al servidor a través de un servicio web, escriba el nombre de usuario y la contraseña requeridos por dicho servicio web.  
  
7.  Escriba un nombre descriptivo para la nueva conexión.  
  
8.  Haga clic en **probar conexión** para comprobar que el servidor está disponible.  
  
## <a name="troubleshooting-connections"></a>Solucionar problemas de las conexiones  
 Esta sección proporciona respuestas a algunas preguntas comunes sobre conexiones con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Aparece un mensaje que indica "no se encontró ninguna conexión".**  
  
 Si el texto de la parte inferior del botón indica que **no hay conexión**, significa que no ha creado una conexión a una [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos o que se ha producido un error en la conexión. Es posible seguir trabajando en Excel con datos de Access u otros orígenes, pero, para crear un modelo de minería de datos o ejecutar una consulta de predicción, es necesario disponer de una conexión activa.  
  
 **¿Supongamos que no tengo permiso para usar el servidor?**  
  
 Si no dispone de los permisos necesarios para almacenar los modelos de minería de datos en el servidor, o si desea probar la minería de datos sin guardar el trabajo, puede utilizar las Herramientas de análisis de tabla, que crean estructuras de datos y modelos temporales. Todavía necesita poder almacenar modelos temporales en el servidor. Pida al administrador que habilite el uso de *modelos de minería de datos de sesión* en el servidor.  
  
 Si desea asegurarse de que los modelos se guardan, puede deshabilitar la opción para utilizar modelos temporales o puede usar los asistentes del Cliente de minería de datos. Estos asistentes almacenan todos los modelos en el servidor. Necesitará acceso administrativo a la base de datos donde se almacenan los modelos, por lo que se recomienda solicitar al administrador la creación de una base de datos especial para crear modelos de minería de datos con los complementos.  
  
 **Perdí la conexión; ¿perdí todo mi trabajo?**  
  
 Si termina la conexión con el servidor, los resultados y los datos no se perderán, ya que se almacenan en Excel. Sin embargo, si ha creado algunos modelos temporales, estos se eliminarán del servidor después de un breve período de tiempo. Por lo tanto, si pierde la conexión temporalmente, los modelos no se eliminarán todavía.  
  
 Los datos o los resultados generados no se perderán, ya que todos los informes y las tablas se almacenan en Excel.  
  
> [!NOTE]  
>  No se desconecte del servidor ni de la red mientras el complemento se esté comunicando con el servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Por ejemplo, no se desconecte nunca mientras se esté creando un modelo o mientras se estén procesando los datos. En algunas situaciones, los datos podrían resultar dañados.  
  
 **No puedo conectarme con el modelo utilizando las herramientas de Visio**  
  
 Las Plantillas de minería de datos para Visio no pueden usar modelos ni estructuras de minería de datos temporales. Para crear un diagrama de un modelo de minería de datos, éste debe estar almacenado en un servidor.  
  
 **¿Cómo puedo supervisar el uso de la conexión?**  
  
 La herramienta [de&#41;de seguimiento &#40;cliente de minería de datos para Excel](trace-data-mining-client-for-excel.md) crea un registro de toda la actividad entre los complementos y el servidor especificado.  
  
 Para habilitar la supervisión de modelos de sesión, seleccione la opción **usar modelos de sesión** en el cuadro de diálogo **seguimiento** .  
  
 El seguimiento le permite ver los comandos DMX y XMLA que se generan mientras se crean modelos y estructuras. También puede ver las consultas enviadas por el cliente para generar resultados e informes en Excel.  
  
 **¿Qué es un modelo temporal? ¿Cómo se puede guardar un modelo temporal?**  
  
 Las Herramientas de análisis de tabla para Excel crean estructuras de datos y modelos de minería de datos temporales de forma predeterminada. Puede continuar examinando y consultando modelos temporales siempre y cuando mantenga el libro abierto y no se desconecte de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 En cuanto cierre el libro de Excel o cambie o finalice la conexión con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], se eliminarán todas las estructuras y modelos de sesión que haya creado.  
  
 Cuando se completa un asistente en el Cliente de minería de datos para Excel, los modelos se guardan en el servidor de forma predeterminada, pero en la última página de cada asistente hay una opción que permite usar un modelo temporal. Si selecciona esta opción, tanto el modelo como la estructura de minería de datos que ha creado se almacenarán en un archivo temporal. Puede examinar, administrar y modificar la estructura y el modelo mientras Excel permanezca abierto. Sin embargo, cuando cierre Excel, se eliminarán la estructura y los modelos relacionados.  
  
 También puede crear explícitamente una estructura o un modelo temporal mediante el **Editor de consultas avanzadas de minería de datos** y seleccionando una de las plantillas DMX. Agregue la cláusula `USE SESSION MODELS` para especificar que los objetos deben ser temporales.   
  
### <a name="creating-backups-of-mining-models-and-structures"></a>Crear copias de seguridad de modelos y estructuras de minería de datos  
 Para crear una copia de seguridad de un modelo o una estructura, puede exportarla mediante el uso de [administrar modelos &#40;SQL Server complementos de minería de datos&#41;](manage-models-sql-server-data-mining-add-ins.md), en el cliente de minería de datos para Excel.  
  
 Si creó un modelo de minería de datos temporal, este normalmente tendrá un nombre que resulta difícil de entender, por ejemplo Table5_593679_TS_62446. Sin embargo, puede usar la herramienta [seguimiento &#40;del cliente de minería de datos para Excel&#41;](trace-data-mining-client-for-excel.md) para detectar los nombres de las estructuras y los modelos temporales creados por las herramientas de análisis de tabla y, a continuación, realizar una copia de seguridad de ellos con **administrar modelos**.  
  
##### <a name="identify-and-export-a-temporary-model"></a>Identificar y exportar un modelo temporal  
  
1.  En el grupo **conexiones** del cliente de minería de datos para Excel, haga clic en **seguimiento**.  
  
2.  Vea el registro de actividad de conexión y busque el modelo revisando las columnas y las salidas de predicción (por ejemplo).  
  
     Usuarios avanzados: si está familiarizado con DMX o XMLA, puede copiar las instrucciones en un archivo para usarlas posteriormente.  
  
3.  Cuando haya encontrado el nombre del modelo y la estructura temporales, Abra **administrar modelo** y seleccione el modelo.  
  
4.  Haga clic en Exportar este modelo de minería de datos para generar un archivo de script en la ubicación que especifique.  
  
## <a name="see-also"></a>Consulte también  
 [Conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md)   
 [Utilidad de configuración del servidor &#40;complementos de minería de datos para Excel&#41;](server-configuration-utility-data-mining-add-ins-for-excel.md)  
  
  
