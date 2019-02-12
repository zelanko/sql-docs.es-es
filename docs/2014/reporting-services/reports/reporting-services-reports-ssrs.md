---
title: Informes de Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, report creation
ms.assetid: 52ed9e74-f2c8-488b-a2c2-6dfbc2a2c8cc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0ae207d14e45c51cee51190bdf0849f0e49d8c05
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56013606"
---
# <a name="reporting-services-reports-ssrs"></a>Informes de Reporting Services (SSRS)
  Los informes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] son definiciones de informe basadas en XML que incluyen los datos y elementos de diseño de los informes. En un sistema de archivos de cliente, las definiciones de informe tienen la extensión de archivo .rdl. Una vez que se publica un informe, se convierte en un elemento de informe que se almacena en el servidor de informes o en el sitio de SharePoint. Los informes constituyen un único componente de la plataforma de generación de informes basada en servidor que proporciona [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 Si está empezando a usar [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], asegúrese de revisar la información en [Conceptos de Reporting Services &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md).  
  
## <a name="benefits-of-reporting-services-reports"></a>Ventajas de los informes de Reporting Services  
 Puede usar las soluciones de informes de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para:  
  
-   Usar un solo conjunto de orígenes de datos que proporcione una única versión de los hechos. Puede basar los informes en esos orígenes de datos para proporcionar una vista de datos unificada que facilite la toma de decisiones comerciales.  
  
-   Visualizar los datos de formas diversas e interconectadas a través de las regiones de datos. Puede mostrar los datos organizados en tablas, matrices o tablas de referencias cruzadas; también puede expandir o contraer grupos, gráficos, medidores, indicadores o KPI, y mapas, e incluso tiene la posibilidad de incluir gráficos en las tablas.  
  
-   Ver los informes para su propio uso o publicar informes en un servidor de informes o un sitio de SharePoint para compartirlos con el equipo o la organización.  
  
-   Definir un informe una sola vez y presentarlo de diversas maneras. Puede exportar el informe en varios formatos de archivo o entregar el informe a los suscriptores en forma de correo electrónico o de un archivo compartido. Puede crear informes vinculados que apliquen distintos conjuntos de parámetros a la misma definición de informe.  
  
-   Usar elementos de informe, orígenes de datos compartidos, consultas compartidas y subinformes para definir las visualizaciones de datos para su reutilización.  
  
-   Administrar los orígenes de datos del informe con independencia de la definición de informe. Por ejemplo, puede cambiar de un origen de datos de prueba a un origen de datos de producción sin cambiar el informe.  
  
-   Crear informes con un diseño libre. El diseño del informe no está restringido a bandas de información. Puede organizar la visualización de los datos de la página de forma que facilite su comprensión, mejore su entendimiento y promueva la entrada en acción.  
  
-   Habilitar acciones para la obtención de detalles, alternadores para expandir y contraer, botones de ordenación, información sobre herramientas y parámetros de informe que permitan al lector interactuar con el informe. Puede combinar los parámetros de informe con sus propias expresiones para que los lectores del informe puedan controlar el modo en que se filtran, agrupan y ordenan los datos.  
  
-   Definir expresiones que le proporcionan la capacidad de personalizar el modo en que se filtran, agrupan y ordenan los datos.  
  
 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")  
  
##  <a name="bkmk_StagesSummary"></a> Fases del procesamiento de informes  
 Al crear un informe, tiene que definir un archivo de definición de informe (.rdl) en formato XML. Este archivo contiene toda la información necesaria para combinar los datos y el diseño del informe mediante el procesador de informes. Cuando consulte un informe, el informe avanzará a través de los pasos siguientes:  
  
-   **Compilación.** Se evalúan las expresiones de la definición de informe y se almacena el formato intermedio compilado internamente en el servidor de informes.  
  
-   **Proceso.** Se ejecutan las consultas de conjuntos de datos y se combina el formato intermedio con los datos y el diseño.  
  
-   **Representación.** El informe procesado se envía a una extensión de representación para determinar cuánta información cabe en cada página y crear el informe paginado.  
  
-   **Exportación (opcional).** El informe se exporta a un formato de archivo diferente.  
  
 Para más información, vea [Fases del desarrollo de los informes](../reporting-services-concepts-ssrs.md#bkmk_StagesofReports) en [Conceptos de Reporting Services &#40;SSRS&#41;](../reporting-services-concepts-ssrs.md).  
  
## <a name="create-reports"></a>Crear informes  
 Para crear un informe:  
  
-   **Determine la finalidad del informe.** Identifique el propósito con el que el público usará el informe. Un informe bien diseñado proporciona información a los lectores que mejorará su entendimiento y les llevará a emprender acciones. Las decisiones de diseño que se tomen durante este paso influirán en la elección de los parámetros, el diseño y la experiencia de visualización del informe. Para más información, vea [Planear un informe &#40;Generador de informes&#41;](../report-design/planning-a-report-report-builder.md) y [Sugerencias para el diseño de informes &#40;Generador de informes y SSRS&#41;](../report-design/report-design-tips-report-builder-and-ssrs.md) en la [documentación del Generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com.  
  
-   **Elija el tipo de consulta.** Determine si se va a usar una consulta de conjunto de datos generalizada y compartida o una consulta específica para el conjunto de informes. Un conjunto de datos compartido con una consulta generalizada resulta fácil de mantener y puede usarse en varios de informes, pero cada diseñador de informes debe filtrar los datos en función de las necesidades de su conjunto de informes particular. Para más información, vea [Datos de informe &#40;SSRS&#41;](../report-data/report-data-ssrs.md).  
  
-   **Planee las vistas de los datos relacionados.** Planee la experiencia de visualización de los lectores del informe. Los informes de resumen con capacidad para profundizar en los detalles constituyen un enfoque útil para administrar grandes volúmenes de datos. Para obtener más información, vea [Obtención de detalles, informes detallados, subinformes y regiones de datos anidadas &#40;Generador de informes y SSRS&#41;](../report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md).  
  
-   **Configure los permisos.** Planee la estrategia de concesión de permisos del nivel adecuado. Una estrategia habitual consiste en crear una estructura de carpetas de servidor de informes y conceder acceso a los informes y a sus elementos relacionados en función de la seguridad de los roles y las carpetas. Para obtener más información, vea [Proteger informes](#bkmk_SecureReportsSummary).  
  
-   **Elija un entorno de creación.** La compatibilidad con las características es distinta en cada herramienta de creación. Para más información, vea [Herramientas de Reporting Services](../tools/reporting-services-tools.md).  
  
-   En cada informe:  
  
    -   **Identifique los orígenes de datos.** Defina los orígenes de datos de los informes, uno por cada origen de datos. Para más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
    -   **Elija qué datos se van a usar de cada origen.** En cada origen de datos, defina los conjuntos de datos del informe. Cada conjunto de datos incluye una consulta que especificará qué datos se van a usar. Si tiene parámetros de informe, defina un conjunto de datos para rellenar la lista de valores disponibles de cada parámetro. Para más información, vea [Agregar datos a un informe &#40;Generador de informes y SSRS&#41;](../report-data/report-datasets-ssrs.md) y [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
    -   **Elija una visualización de los datos.** En cada conjunto de datos, elija qué región de datos se va a usar para mostrar los datos. Elija en la lista de tablas, gráficos, medidores y mapas. Para obtener más información, vea los temas siguientes:  
  
        -   [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](../report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)  
  
        -   [Gráficos &#40;Generador de informes y SSRS&#41;](../report-design/charts-report-builder-and-ssrs.md)  
  
        -   [Minigráficos y barras de datos &#40;Generador de informes y SSRS&#41;](../report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)  
  
        -   [Indicadores &#40;Generador de informes y SSRS&#41;](../report-design/indicators-report-builder-and-ssrs.md)  
  
        -   [Mapas &#40;Generador de informes y SSRS&#41;](../report-design/maps-report-builder-and-ssrs.md)  
  
        -   [Medidores &#40;Generador de informes y SSRS&#41;](../report-design/gauges-report-builder-and-ssrs.md)  
  
    -   **Personalice los datos y el diseño.** Cree el diseño del informe. Una definición de informe tiene un cuerpo, orígenes de datos, conjuntos de datos, regiones de datos, cuadros de texto, líneas e imágenes de informe. Los rectángulos se usan como contenedores de diseño, además de como elementos visuales. Personalice cada región de datos escribiendo expresiones para controlar el filtrado, la agrupación, la ordenación, el formato y la visualización de los datos. Agregue los nombres, las ubicaciones y otra información de identificación del informe que ayude a administrar docenas o cientos de informes. Agregue los elementos visuales y los contenedores para organizar los elementos de diseño de la página. Para obtener más información, vea los temas siguientes:  
  
        -   [Filtrar, agrupar y ordenar datos &#40;Generador de informes y SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
        -   [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
        -   [Expresiones &#40;Generador de informes y SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
        -   [Aplicar formato a los elementos de informe &#40;Generador de informes y SSRS&#41;](../report-design/formatting-report-items-report-builder-and-ssrs.md)  
  
        -   [Imágenes, cuadros de texto rectángulos y líneas &#40;Generador de informes y SSRS&#41;](../report-design/rectangles-and-lines-report-builder-and-ssrs.md)  
  
        -   [Representación y diseño de páginas &#40;Generador de informes y SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md)  
  
    -   **Configure las características de interactividad.** Agregue características de interactividad para los lectores del informe. Por ejemplo, agregue botones de ordenación o elementos de alternancia para ver las consultas. Para más información, vea [Ordenación interactiva, mapas de documento y vínculos &#40;Generador de informes y SSRS&#41;](../report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md).  
  
    -   **Revise y repita el diseño.** Obtenga una vista previa del informe. Publique una versión preliminar para obtener comentarios de los lectores del informe. Repita el diseño.  
  
-   **Revise una solución de generación de informes.** Compruebe que el conjunto de informes interactúa correctamente.  
  
-   **Considere qué componentes pueden reutilizarse.**  Determine si alguno de los orígenes de datos o consultas de conjuntos de datos pueden compartirse para su reutilización. Si es así, en el servidor de informes o en el sitio de SharePoint, cree orígenes de datos compartidos y conjuntos de datos compartidos. Determine si las regiones de datos son adecuadas para reutilizarlas como elementos de informe. Para obtener más información, vea [Elementos de informe en el Diseñador de informes &#40;SSRS&#41;](../report-design/report-parts-in-report-designer-ssrs.md).  
  
## <a name="preview-reports"></a>Obtener una vista previa de los informes  
 Todas las herramientas de generación de informes admiten la vista previa de los informes. Para más información, vea [Vista previa](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_Preview), [Generador de informes &#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md) y [Mostrar la vista previa de informes en el Generador de informes](../report-builder/previewing-reports-in-report-builder.md) en la [documentación del Generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com.  
  
## <a name="save-or-publish-reports"></a>Guardar o publicar informes  
 Todas las herramientas de generación de informes permiten guardar los informes localmente y publicarlos en un servidor de informes o en un sitio de SharePoint. Para más información, vea [Guardar e implementar](../tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md#bkmk_SaveandDeploy), [Generador de informes &#40;SSRS&#41;](../tools/report-builder-authoring-environment-ssrs.md) y [Guardar informes &#40;Generador de informes&#41;](../report-builder/saving-reports-report-builder.md) en la [documentación del Generador de informes](https://go.microsoft.com/fwlink/?LinkId=154494) en msdn.microsoft.com.  
  
## <a name="view-reports"></a>Ver informes  
 Además de mostrar una vista previa de un informe guardado localmente o publicado en un servidor de informes, puede proporcionar diversas experiencias de visualización a los lectores del informe. Para ver un informe:  
  
-   **Explorador.**  Use el servicio web del servidor de informes o del sitio de SharePoint para ver los informes publicados. En un sitio de SharePoint, también puede configurar un elemento web para ver los informes publicados. Para más información, vea [Planear la compatibilidad del explorador de Reporting Services y Power View &#40;Reporting Services 2014&#41;](../browser-support-for-reporting-services-and-power-view.md), [Administrador de informes &#40;Modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md) y [Acceso URL &#40;SSRS&#41;](../url-access-ssrs.md).  
  
-   **Entrega.**  Configure una suscripción para entregar informes a los lectores a través de un mensaje de correo electrónico o una carpeta de archivos compartida.  Para obtener más información, vea [Suscripciones y entrega &#40;Reporting Services&#41;](../subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
-   **Exportación.**  En la barra de herramientas del visor de informes, un lector puede exportar un informe a un formato de archivo diferente. Los formatos de archivo de exportación los puede configurar el administrador del servidor de informes. Para más información, vea [Exportación de informes &#40;Generador de informes y SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md).  
  
-   **Impresión.**  Un lector de informes puede imprimir un informe o algunas de las páginas de un informe, en función del modo en que lo esté viendo. Para más información, vea [Imprimir informes &#40;Generador de informes y SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md).  
  
-   **Aplicación web o formulario Windows Forms.**  Use Visual Studio para desarrollar una aplicación ASP.NET AJAX o una aplicación de Windows Forms que hospede el control de visor de informes. El control puede apuntar a informes publicados en un servidor de informes. Para obtener más información, vea [Informes de Microsoft](https://go.microsoft.com/fwlink/?LinkID=205399).  
  
## <a name="manage-reports"></a>Administrar informes  
 Para administrar un informe publicado:  
  
-   **Orígenes de datos.** Los orígenes de datos compartidos e incrustados se administran independientemente de la definición de informe.  
  
-   **Conjuntos de datos.**  Los conjuntos de datos compartidos se administran con independencia de la definición de informe.  
  
-   **Parámetros.**  Los parámetros se administran con independencia de la definición de informe. Una vez que los parámetros se modifican en el servidor de informes, los clientes de generación de informes no pueden publicar los cambios realizados en el servidor.  
  
-   **Recursos.**  Las imágenes y los datos espaciales de los archivos de forma ESRI son recursos que se pueden publicar y administrar con independencia de la definición de informe.  
  
-   **Memoria caché de informes.**  Mediante la programación de informes de gran tamaño que se van a ejecutar durante las horas de menor actividad, puede reducir el impacto del procesamiento en el servidor de informes durante las principales horas comerciales.  
  
-   **Instantáneas.**  Use instantáneas de informe cuando desee proporcionar resultados coherentes para varios usuarios que deben trabajar con conjuntos de datos idénticos. Si los datos no son estables, un informe a petición puede producir resultados diferentes en pocos minutos. Por el contrario, una instantánea de informe permite hacer comparaciones válidas con otros informes o herramientas de análisis que tengan los datos existentes en el mismo instante.  
  
-   **Historial del informe.** Mediante la creación de una serie de instantáneas de informe, puede crear el historial de un informe que muestre cómo cambian los datos en el transcurso del tiempo.  
  
 Para más información sobre rendimiento, vea [Rendimiento, instantáneas, almacenamiento en caché &#40;Reporting Services&#41;](../report-server/performance-snapshots-caching-reporting-services.md).  
  
##  <a name="bkmk_SecureReportsSummary"></a> Proteger informes  
 Para proteger un informe:  
  
-   En el administrador del servidor de informes, identifique el sistema de autorización y autenticación empleado para la instalación de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . De forma predeterminada, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa la autenticación de Windows, la seguridad integrada y la asignación de roles para ayudar a controlar el acceso a los informes publicados. Para más información, vea [Roles y permisos &#40;Reporting Services&#41;](../security/roles-and-permissions-reporting-services.md) y [Seguridad y protección de Reporting Services](../security/reporting-services-security-and-protection.md).  
  
## <a name="create-notifications-based-on-report-data"></a>Crear notificaciones basadas en datos del informe  
 Puede crear alertas de datos de los informes publicados en un sitio de SharePoint. Las alertas de datos se basan en las fuentes de distribución de datos de las regiones de datos del informe. De forma predeterminada, las regiones de datos se asignan automáticamente. Los autores de informes pueden facilitar la creación de alertas de datos en sus informes asignando los nombres de las regiones de datos en función de su objetivo comercial. Cuando cree una alerta de datos, recibirá un mensaje de correo electrónico en el que se le notificará cuándo los datos cumplen las condiciones especificadas. Para más información, vea [Generar fuentes de distribución de datos a partir de informes &#40;Generador de informes y SSRS&#41;](../report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md), [Crear una alerta de datos en el Diseñador de alertas de datos](../create-a-data-alert-in-data-alert-designer.md) y [Alertas de datos de Reporting Services](../reporting-services-data-alerts.md).  
  
## <a name="upgrade-reports"></a>Upgrade Reports  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] admite varias versiones de las definiciones de informe, de los servidores de informes y de los sitios de SharePoint. Para actualizar un informe:  
  
-   Actualice una instalación del servidor de informes. Los informes compilados que se almacenan en el servidor de informes se actualizan automáticamente al usarse por primera vez. La definición de informe (.rdl) no se modifica. Para obtener más información, vea [Upgrade and Migrate Reporting Services](../install-windows/upgrade-and-migrate-reporting-services.md).  
  
-   Abra un informe en un entorno de creación de informes. La definición de informe se actualiza en la mayoría de los casos. Para más información, vea [Actualizar informes](../install-windows/upgrade-reports.md) e [Implementación y compatibilidad de versiones en SQL Server Data Tools &#40;SSRS&#41;](../tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
## <a name="troubleshoot-reports"></a>Solucionar problemas de informes  
 Para solucionar los problemas de un informe:  
  
-   **Determine dónde se está produciendo el problema.** Revise la información incluida en [Etapas de un informe](#bkmk_StagesSummary).  
  
-   **Determine dónde puede buscar más información.** Por ejemplo, si el diseño de informe incluye expresiones, la herramienta Diseñador de informes proporciona más información sobre los problemas de evaluación de expresiones que la herramienta Generador de informes. Si se producen errores de procesamiento de informes, los archivos de registro contienen información detallada.  
  
## <a name="tasks"></a>Tareas  
 Para buscar vínculos a temas paso a paso, vea la sección Tareas de los artículos de características mencionados en las secciones anteriores de este tema.  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de Reporting Services](../tools/reporting-services-tools.md)   
 [Extensiones &#40;SSRS&#41;](../extensions-ssrs.md)   
 [Servidor de informes de Reporting Services](../reporting-services-report-server.md)  
  
  
