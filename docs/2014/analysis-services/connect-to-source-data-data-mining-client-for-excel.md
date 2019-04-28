---
title: Conectarse al origen de datos (cliente de minería de datos para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
ms.assetid: 548672ce-e403-4aca-b67a-c2c797f053dd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 78c60832ea6111b0682e8a6d2b5ab3540a19cfb1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62680266"
---
# <a name="connect-to-source-data-data-mining-client-for-excel"></a>Conectar con los datos de origen (Cliente de minería de datos para Excel)
  En este tema se describe cómo crear y usar las conexiones utilizadas para almacenar modelos de minería de datos y para obtener acceso a datos externos almacenados en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Conexiones de minería de datos.** La conexión inicial que crea cuando inicia los complementos se usa para obtener acceso a los algoritmos, analizar los datos y almacenar modelos y estructuras de minería de datos.  
  
 Se requiere una conexión a una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para usar las herramientas de modelado y de visualización en los complementos, ya que los complementos dependen de los algoritmos y estructuras de datos que proporciona [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Conexiones a orígenes de datos externos.** También puede crear conexiones a datos externos mientras crea modelos o guarda resultados. Por ejemplo, puede crear un modelo de minería de datos en un servidor y, a continuación, realizar una consulta de predicción a partir de ese modelo de minería de datos usando los datos almacenados en otra instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], en una tabla de datos de Excel o en un origen de datos externo, como [!INCLUDE[msCoName](../includes/msconame-md.md)] Access. Cada vez que obtenga acceso al nuevo origen de datos, se le pedirá que cree una conexión mediante un cuadro de diálogo.  
  
##  <a name="bkmk_prereq2"></a> Requisitos previos  
 Esta versión de los complementos requiere que la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] sea SQL Server 2012. Si desea conectarse a una versión anterior de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], tiene a su disposición otra versión de los complementos. Existen versiones de los complementos que admiten SQL Server 2005, SQL Server 2008 y SQL Server 2008 R2.  
  
 Para conectarse a una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], debe tener permisos para obtener acceso al servidor de base de datos. Además, las sesiones de minería de datos deben estar habilitadas y se debe contar con permisos de lectura o de lectura y escritura en los objetos de base de datos almacenados en el servidor.  
  
##  <a name="bkmk_connect"></a> Creación de conexiones de servidor de minería de datos  
 El **conexiones** grupo en el cliente de minería de datos para Excel y las herramientas de análisis de tabla para Excel proporciona herramientas para administrar las conexiones a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
-   Puede crear la conexión cuando instale el complemento o agregar una conexión posteriormente.  
  
-   Puede crear varias conexiones y modificar las conexiones en cualquier momento, a menos que esté en el proceso de crear o consultar un modelo.  
  
     No cambie ni cierre una conexión cuando se esté procesando un modelo de minería de datos. El modelo de minería de datos podría perder datos o quedar inutilizable.  
  
-   Solo puede haber una conexión activa de cada vez.  
  
### <a name="connections-in-the-excel-add-ins"></a>Conexiones en los complementos de Excel  
 El **conexiones** grupo en el cliente de minería de datos para Excel y las herramientas de análisis de tabla para Excel es donde administra las conexiones a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
##### <a name="create-a-new-server-connection-in-the-excel-add-ins"></a>Crear una nueva conexión al servidor en los complementos de Excel  
  
1.  Haga clic en el **conexión** situado en la **analizar** o **minería de datos** cinta de opciones.  
  
    > [!NOTE]  
    >  El texto del botón indica si existe una conexión. Cuando no se ha realizado ninguna conexión en la hoja de cálculo, el botón contiene el texto "\<ninguna conexión >." Si se estableció una conexión previamente en el libro, el nombre de ésta aparece en el botón.  
  
2.  En el **conexiones de Analysis Services** cuadro de diálogo, haga clic en **New**.  
  
3.  En el **nueva conexión de Analysis Services** diálogo cuadro, escriba el nombre del servidor.  
  
4.  Especifique el método de autenticación.  
  
5.  Seleccione una base de datos desde el **CatalogName** lista desplegable. Si no existe ninguna base de datos en la instancia, seleccione **(valor predeterminado)**.  
  
6.  Escriba un nombre descriptivo para la conexión.  
  
7.  Haga clic en **Probar conexión** para comprobar que el servidor y base de datos están disponibles.  
  
8.  Haga clic en **Aceptar**y, a continuación, en **Cerrar**.  
  
### <a name="connections-using-a-web-service"></a>Conexiones mediante un servicio web  
 Si usa una arquitectura de cliente ligero para habilitar la exploración de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cubos y los datos, también puede configurar una conexión a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] servidor a través de servicios Web. Para obtener información acerca de cómo definir un cliente basado en web, vea los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Si dispone de acceso a un servidor configurado para servicios Web, podrá especificar el tipo de conexión cuando la cree por primera vez.  
  
##### <a name="create-an-http-connection-to-analysis-services"></a>Crear una conexión HTTP a Analysis Services  
  
1.  Abra el **nueva conexión de Analysis Services** cuadro de diálogo.  
  
2.  Para el nombre del servidor, escriba http:// seguido de la dirección URL asignada al servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Escriba el nombre de usuario y la contraseña necesarios para obtener acceso al servicio web.  
  
### <a name="connections-in-the-visio-add-in"></a>Conexiones en el complemento de Visio  
 A diferencia de Excel, Visio no dispone de una cinta de opciones de herramientas ni de botones específicos para crear o supervisar conexiones. En su lugar, la conexión de datos se crea cuando se selecciona por vez primera una forma de minería de datos y se coloca en una página de Visio. Un asistente le solicitará que seleccione el modelo para la forma y que establezca otras opciones.  
  
 Si ya ha usado conexiones a un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en Excel con anterioridad, estas aparecen como posibles orígenes de datos entre los que puede elegir.  
  
##### <a name="create-a-connection-for-a-visio-shape"></a>Crear una conexión para una forma de Visio  
  
1.  Abra la plantilla de minería de datos y seleccione una de las formas de minería de datos.  
  
2.  Arrastre la forma y colóquela en una página en blanco.  
  
3.  En el **seleccionar un origen de datos** cuadro de diálogo, seleccione una de datos de origen en la lista o haga clic en **New**.  
  
4.  Si selecciona **New**, siga el procedimiento descrito anteriormente para especificar un servidor y el nombre del catálogo, o se conecten a través de un servicio Web.  
  
##  <a name="bkmk_change"></a> Cambio de conexiones  
 Es posible crear varias conexiones en la misma hoja de cálculo, aunque sólo puede haber una activa en cada momento. El nombre de la conexión actual se muestra en el **conexión** botón.  
  
 En el cliente de minería de datos para Excel, también puede comprobar la cadena de conexión y el estado de la conexión actual, haga clic en **seguimiento** y, a continuación, haga clic en **conexión actual**.  
  
#### <a name="use-a-different-server-connection"></a>Usar una conexión al servidor diferente  
  
1.  Haga clic en **conexión**.  
  
2.  En el **conexiones de Analysis Services** panel, seleccione una conexión desde el **otras conexiones** lista y haga clic en **convertir en actual**.  
  
3.  Haga clic en **Probar conexión** para comprobar que la conexión está disponible.  
  
 Una vez que un modelo de minería de datos ha finalizado el procesamiento, los resultados se almacenan localmente; si se cierra la conexión con un servidor y se establece la conexión con otro, los datos no resultarán afectados. No obstante, se debe evitar el cambio de conexión o la pérdida de la misma mientras se está procesando un modelo de minería de datos, ya que los datos podrían resultar dañados.  
  
#### <a name="modify-an-existing-server-connection"></a>Modificar una conexión al servidor existente  
  
1.  No puede modificar una conexión existente; si desea conectarse a una base de datos o a un servidor diferente, debe crear una conexión nueva.  
  
2.  Si debe modificar la cadena de conexión para aumentar el tiempo de espera de consulta o para agregar otros parámetros específicos para la instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], una opción es modificar el archivo .dmc, donde se almacena la cadena de conexión.  
  
     \<unidad: > \Users\\< myusername\>\AppData\Local\Microsoft\Data complemento de minería de datos  
  
##  <a name="bkmk_extconnections"></a> Conectarse a orígenes de datos externos  
 Mientras que las herramientas de la **analizar** funcionan exclusivamente con datos en Excel, las herramientas de la cinta de opciones la **minería de datos** cinta de opciones le permite conectarse directamente a orígenes de datos externos que se usará como entradas para el modelo, o para muestreo.  
  
 Las siguientes herramientas de estos complementos admiten el uso de datos externos para minería de datos:  
  
-   [Datos de ejemplo &#40;complementos de minería de datos de SQL Server&#41;](sample-data-sql-server-data-mining-add-ins.md)  
  
-   [Asistente para clasificar &#40;datos complementos de minería de datos para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Asistente para estimación &#40;datos complementos de minería de datos para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Asistente para clúster &#40;datos complementos de minería de datos para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Asistente para pronóstico &#40;datos complementos de minería de datos para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Crear estructura de minería de datos &#40;complementos de minería de datos de SQL Server&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
-   [Gráfico de precisión &#40;complementos de minería de datos de SQL Server&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
-   [Gráfico de beneficios &#40;complementos de minería de datos de SQL Server&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
  
-   [Matriz de clasificación &#40;complementos de minería de datos de SQL Server&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
### <a name="using-analysis-services-as-a-data-source"></a>Usar Analysis Services como un origen de datos  
 No puede tener acceso directamente a los datos almacenados en un cubo o modelo tabular de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. En su lugar, cree una conexión en Excel al servidor de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] y use los datos para crear un modelo.  
  
### <a name="relational-data-sources"></a>Orígenes de datos relacionales  
 Si desea usar los datos de un origen relacional como entrada para el modelo, puede conectarse a las versiones siguientes de SQL Server:  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
 También puede obtener datos de cualquier otro origen de datos relacional que admita [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] como origen de datos. Para obtener información acerca de los orígenes de datos admitidos, vea [orígenes de datos en modelos multidimensionales](multidimensional-models/data-sources-in-multidimensional-models.md)  
  
 Tenga en cuenta que los siguientes tipos de datos no se pueden usar para minería de datos y producirán un error si se incluyen al crear un modelo:  
  
-   ntext  
  
-   binary  
  
## <a name="see-also"></a>Vea también  
 [Seguimiento &#40;cliente de minería de datos para Excel&#41;](trace-data-mining-client-for-excel.md)  
  
  
