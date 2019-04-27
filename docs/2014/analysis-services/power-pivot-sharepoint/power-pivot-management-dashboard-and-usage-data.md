---
title: PowerPivot Management Dashboard and Usage Data | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 541c8b1f-c6c2-423d-a97d-65c379967e0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cf132a6cd6e15002b36ba7ecdced512e3686e433
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748906"
---
# <a name="powerpivot-management-dashboard-and-usage-data"></a>Panel de administración de PowerPivot y datos de uso
  El Panel de administración de PowerPivot es una colección de informes predefinidos y elementos web de Administración central de SharePoint que ayudan a administrar una implementación de SQL Server PowerPivot para SharePoint. El Panel de administración proporciona información relacionada con el estado del servidor, la actividad de los libros y la actualización de datos. El panel usa datos de la recopilación de datos de uso de SharePoint.  
  
 [Requisitos previos](#prereq)  
  
 [Descripción de las secciones del panel](#items)  
  
 [Panel de administración de PowerPivot abiertos](#open)  
  
 [Datos de origen en paneles](#sourcedata)  
  
 [Modificar el panel de PowerPivot](#edit)  
  
 [Crear informes personalizados para el panel de administración de PowerPivot](#reports)  
  
##  <a name="prereq"></a> Requisitos previos  
 Debe ser administrador de servicios si desea abrir el Panel de administración de PowerPivot para una aplicación de servicio PowerPivot que administre.  
  
##  <a name="items"></a> Información general de las secciones del panel  
 El panel de administración de PowerPivot contiene elementos webs e informes incrustados que detallan categorías de información concretas. En la lista siguiente se describen todas las partes del panel:  
  
|Panel|Descripción|  
|---------------|-----------------|  
|Infraestructura: estado del servidor|Muestra las tendencias de uso de la CPU, el consumo de memoria y los tiempos de respuesta de las consultas a lo largo del tiempo para poder evaluar si los recursos del sistema se están acercando a la capacidad máxima o están infrautilizados.|  
|Acciones|Contiene vínculos a otras páginas de Administración central, incluida la aplicación de servicio actual, una lista de aplicaciones de servicio y registro de uso.|  
|Actividad de libro: gráfico|Notifica la frecuencia de acceso a los datos. Puede obtener información acerca de la frecuencia con que se producen conexiones a los orígenes de datos PowerPivot diaria o semanalmente.|  
|Actividad de libro: lista|Notifica la frecuencia de acceso a los datos. Puede obtener información acerca de la frecuencia con que se producen conexiones a los orígenes de datos PowerPivot diaria o semanalmente.|  
|Actualización de datos: actividad reciente|Los informes del estado de los trabajos de actualización de datos, incluso de los que no pudieron ejecutarse. Este informe proporciona una vista compuesta en las operaciones de actualización de datos en el nivel de aplicación. Los administradores pueden ver de un vistazo el número de trabajos de actualización de datos que están definidos para toda la aplicación de servicio PowerPivot.|  
|Actualización de datos: errores recientes|Enumera los libros PowerPivot que no completaron la actualización de datos correctamente.|  
|Informes|Contiene los vínculos a los informes que se pueden abrir en Excel.|  
  
##  <a name="open"></a> Panel de administración de PowerPivot abiertos  
 El panel muestra información sobre una aplicación de servicio PowerPivot cada vez. Puede abrir el panel de administración desde dos ubicaciones distintas.  
  
### <a name="open-the-dashboard-from-general-application-settings"></a>Abrir el panel desde Configuración de aplicación general  
  
1.  En Administración central, en el grupo **Configuración de aplicación general** , haga clic en **Panel de administración de PowerPivot**.  
  
2.  En la página principal, seleccione la aplicación de servicio PowerPivot para la que desea ver los datos de las operaciones.  
  
### <a name="open-the-dashboard-from-a-powerpivot-service-application"></a>Abrir el panel desde una aplicación de servicio PowerPivot  
  
1.  En Administración central, en **Administración de aplicaciones**, haga clic en **Administrar las aplicaciones de servicio**.  
  
2.  Haga clic en el nombre de la aplicación de servicio PowerPivot. El Panel de administración de PowerPivot muestra datos operativos sobre la aplicación de servicio actual.  
  
### <a name="change-the-current-service-application"></a>Cambiar la aplicación de servicio actual  
 Para cambiar la aplicación de servicio PowerPivot actual en el panel de administración:  
  
1.  En la parte superior del panel de administración de PowerPivot, observe el nombre de la aplicación de servicio actual, por ejemplo **aplicación de servicio PowerPivot predeterminada**.  
  
2.  En el panel **Acciones** , haga clic en **Enumerar aplicaciones de servicio**.  
  
3.  Haga clic en el nombre de la aplicación de servicio PowerPivot para la que desee ver informes del panel de administración.  
  
##  <a name="sourcedata"></a> Datos de origen en paneles  
 Los paneles, informes y elementos web muestran datos de un modelo de datos interno que extrae datos del sistema y de las bases de datos de aplicación de PowerPivot. El modelo de datos interno se incrusta en un libro PowerPivot hospedado en el sitio de administración central. La estructura del modelo de datos es fija. Aunque puede usar el libro PowerPivot como origen de datos para crear informes nuevos, no debe modificar la estructura de ningún modo que perjudique los informes predefinidos que la emplean.  
  
 Para obtener más información acerca de cómo se recopilan los datos, vea lo siguiente:  
  
-   [Recopilación de datos de uso de PowerPivot](power-pivot-usage-data-collection.md)  
  
-   [Configurar la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
 Para capturar datos acerca del sistema de servidor de PowerPivot, compruebe que la mensajería de eventos, el historial de actualización de datos y otros historiales de uso están habilitados para todas las aplicaciones de servicio PowerPivot. Los datos de uso y de servidor recopilados durante las operaciones normales del servidor son los datos de origen que terminan en el modelo de datos interno. **Nota:** Si desactiva el historial de uso o de eventos, los informes compuestos estarán incompletos o serán erróneos.  
  
##  <a name="edit"></a> Modificar el panel de PowerPivot  
 Si tiene experiencia en el desarrollo o personalización de paneles, puede modificar un panel para incluir las nuevas partes web. También puede editar las propiedades de los elementos web que se incluyen en el panel.  
  
##  <a name="reports"></a> Crear informes personalizados para el panel de administración de PowerPivot  
 Para el informe de errores, se conserva el historial y los datos de uso de PowerPivot en un libro PowerPivot interno que se crea y configura junto con el panel. Si los informes predeterminados no proporcionan la información que requiere, puede crear informes personalizados en Excel que se basen en el libro. Si actualiza o desinstala los archivos de solución de PowerPivot más tarde, se conservarán tanto el libro como cualquier informe personalizado que cree. El libro y los informes se almacenan en la biblioteca de administración de PowerPivot dentro del sitio de administración central. Esta biblioteca no es visible de forma predeterminada, pero puede verla si usa la acción Ver todo el contenido del sitio en Acciones del sitio.  
  
 Para ayudarle a empezar a trabajar rápidamente con informes personalizados, el Panel de administración de PowerPivot proporciona un archivo de conexión de datos de Office (.odc) para conectar con el libro de origen. Por ejemplo, puede usar el archivo .odc en Excel para crear informes adicionales.  
  
> [!NOTE]  
>  Edite el archivo para evitar el error siguiente al intentar usar el archivo .odc en Excel: "Error de inicialización del origen de datos". El archivo .odc generado automáticamente incluye un parámetro que el proveedor OLE DB MSOLAP no admite. Las siguientes instrucciones proporcionan la solución alternativa para quitar los parámetros.  
  
 Debe ser un administrador de granja o de servicio para compilar informes que estén basados en el libro PowerPivot en la administración central.  
  
1.  Abra el panel de administración de PowerPivot.  
  
2.  Desplácese a la sección **Informes** en la parte inferior de la página.  
  
3.  Haga clic en **Datos de administración de PowerPivot**.  
  
4.  Guarde el archivo .odc en una carpeta local.  
  
5.  Abra el archivo .odc en un editor de texto.  
  
6.  En el elemento `<odc:ConnectionString>`, desplácese al final de la línea y quite `Embedded Data=False` y, a continuación, quite `Edit Mode=0`. Si el último carácter en la cadena es un punto y coma, quítelo ahora.  
  
7.  Guarde el archivo. Los pasos restantes serán distintos según la versión de PowerPivot y de Excel que esté usando.  
  
8.  1.  Inicie Excel 2013  
  
    2.  En la cinta de **PowerPivot** , haga clic en **Administrar**.  
  
    3.  Haga clic en **Obtener datos externos** y, a continuación, haga clic en **Conexiones existentes**.  
  
    4.  Haga clic en el archivo .ODC si lo ve. Si no ve el archivo .ODC, haga clic en **Buscar más** y, a continuación, en la ruta de acceso de archivo, especifique el archivo .odc.  
  
    5.  Haga clic en **Abrir**.  
  
    6.  Haga clic en **Probar conexión** para comprobar que la conexión se realizó correctamente.  
  
    7.  Escriba un nombre para la conexión y, a continuación, haga clic en **Siguiente**.  
  
    8.  En especificar una consulta MDX, haga clic en **diseño** para abrir el Diseñador de consultas MDX para ensamblar los datos que desea trabajar con **si ve el mensaje de error** "el nombre de propiedad del modo de edición no se formateó correctamente.", compruebe que las modificaciones del. Archivo ODC.  
  
    9. Haga clic en **Aceptar** y, a continuación, haga clic en **Finalizar**.  
  
    10. Cree informes de tabla dinámica o de gráfico dinámico para visualizar los datos en Excel.  
  
9. 1.  Inicie Excel 2010.  
  
    2.  En la cinta de PowerPivot, haga clic en **Iniciar ventana de PowerPivot**.  
  
    3.  En la cinta de opciones Diseño de la ventana de PowerPivot, haga clic en **Conexiones existentes**.  
  
    4.  Haga clic en **Buscar más**.  
  
    5.  En la ruta de acceso al archivo, especifique el archivo .odc.  
  
    6.  Haga clic en **Abrir**. Se abre el Asistente para la importación de tablas, usando la cadena de conexión con el libro PowerPivot que contiene los datos de uso.  
  
    7.  Haga clic en **Probar conexión** para comprobar que tiene acceso.  
  
    8.  Escriba un solo nombre para la conexión y, a continuación, haga clic en **Siguiente**.  
  
    9. En Especificar una consulta MDX, haga clic en **Diseño** para abrir el diseñador de consultas MDX con el fin de ensamblar los datos con los que desea trabajar y, a continuación, cree un informe de tabla dinámica o de gráfico dinámico para visualizar los datos en Excel.  
  
## <a name="see-also"></a>Vea también  
 [Actualización de datos PowerPivot con SharePoint 2010](../powerpivot-data-refresh-with-sharepoint-2010.md)   
 [Configurar la recopilación de datos de uso para &#40;PowerPivot para SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
