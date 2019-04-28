---
title: Cambios de comportamiento en Analysis Services las características de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 92ebd5cb-afb6-4b62-968f-39f5574a452b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0f7cc154a79a329bc18d02535e3f3332aa7e8b61
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62655848"
---
# <a name="behavior-changes-to-analysis-services-features-in-sql-server-2014"></a>Cambios de comportamiento en las características de Analysis Services en SQL Server 2014
  Este tema describe los cambios de comportamiento en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para la minería de datos multidimensional, tabular y las implementaciones de [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] . Los cambios de comportamiento afectan a cómo funcionan o interactúan las características en la versión actual en comparación con las versiones anteriores de SQL Server.  
  
> [!NOTE]  
>  En cambio, un cambio principal es aquel que evita que un modelo de datos o aplicación integrada con [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se ejecute. Para obtener más información, vea [Breaking Changes to Analysis Services Features in SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md).  
  
 En este tema:  
  
-   [Cambios de comportamiento en SQL Server 2014](#bkmk_sql2014)  
  
-   [Cambios de comportamiento en SQL Server 2012 SP1](#bkmk_sql2012sp1)  
  
-   [Cambios de comportamiento en SQL Server 2012](#bkmk_sql2012)  
  
##  <a name="bkmk_sql2014"></a> Cambios de comportamiento en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Hay ningún cambio de comportamiento nuevo anunciado para la minería de datos tabulares, multidimensionales o las características de [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] de esta versión.  Sin embargo, como  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] es tan similar a las versiones [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] , los cambios de comportamiento de ambas versiones anteriores se proporcionan aquí por comodidad en caso de que esté actualizando desde [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
##  <a name="bkmk_sql2012sp1"></a> Cambios de comportamiento en [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]  
 En esta sección se documentan los cambios de comportamiento notificados para las características de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]. Estos cambios también se aplican a [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
|Problema|Descripción|  
|-----------|-----------------|  
|Los libros de SQL Server 2008 R2 PowerPivot no actualizarán automáticamente los modelos cuando se usen en SQL Server 2012 SP1 PowerPivot para SharePoint 2013. Por tanto, las actualizaciones de datos programadas no funcionarán para los libros de SQL Server 2008 R2 PowerPivot.|Los libros de SQL Server 2008 R2 se abrirán en [!INCLUDE[ssGeminiShortvnext](../includes/ssgeminishortvnext-md.md)], pero las actualizaciones programadas no funcionarán. Si examina el historial de actualización verá un mensaje de error similar al siguiente:<br /> "El libro contiene un modelo de PowerPivot no admitido. El modelo de PowerPivot del libro tiene el formato de SQL Server 2008 R2 PowerPivot para Excel 2010. Los modelos de PowerPivot admitidos son los siguientes: <br />SQL Server 2012 PowerPivot para Excel 2010<br />SQL Server 2012 PowerPivot para Excel 2013"<br /><br /> **Cómo actualizar un libro:** Las actualizaciones programadas no funcionarán hasta que actualice el libro a un libro de 2012. Para actualizar el libro y el modelo que contiene, complete una de las acciones siguientes:<br /><br /> Descargue y abra el libro en Microsoft Excel 2010 con el complemento SQL Server 2012 PowerPivot para Excel instalado. Después, guarde el libro y vuelva a publicarlo en el servidor de SharePoint.<br /><br /> Descargue y abra el libro en Microsoft Excel 2013. Después, guarde el libro y vuelva a publicarlo en el servidor de SharePoint.<br /><br /> <br /><br /> Para obtener más información sobre la actualización del libro, consulte [actualizar libros y actualización de datos programada &#40;SharePoint 2013&#41;](instances/install-windows/upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013.md).|  
|Cambios de comportamiento en [ALL Function](https://msdn.microsoft.com/library/ee634802(v=sql.120).aspx)de DAX|Antes de [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)], si especifica una columna [Date] en una tabla Marcar como tabla de fechas, para usarla en inteligencia temporal y esa columna [Date] se pasa como argumento a la función ALL, a su vez, pasada como un filtro a una función CALCULATE, todos los filtros de todas las columnas de la tabla se omiten, con independencia de cualquier segmentación en esa columna de fechas.<br /><br /> Por ejemplo,<br /><br /> `= CALCULATE (<expression>, ALL (DateTable[Date]))`<br /><br /> Antes de [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)], todos los filtros se omitían para todas las columnas de DateTable, con independencia de la columna [Date] pasada como argumento a ALL.<br /><br /> En [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] y en PowerPivot in Excel 2013, el comportamiento omitirá los filtros solo para la columna especificada pasada como argumento a ALL.<br /><br /> Para evitar el nuevo comportamiento, y en efecto omitir todas las columnas como un filtro para la tabla entera, puede excluir la columna [Date] del argumento, por ejemplo,<br /><br /> `=CALCULATE (<expression>, ALL(DateTable))`<br /><br /> Esto dará el mismo resultado que el comportamiento anterior a [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)].|  
  
##  <a name="bkmk_sql2012"></a> Cambios de comportamiento en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 En esta sección se documentan los cambios de comportamiento notificados para las características de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Estos cambios también se aplican a [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
### <a name="analysis-services-multidimensional-mode"></a>Analysis Services, modo multidimensional  
  
#### <a name="nullprocessing-option-set-to-preserve-is-no-longer-supported-for-distinct-count-measures"></a>La opción NullProcessing establecida como Preserve ya no se admite para las medidas de recuento distintivas  
 Anteriores a [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], era posible establecer [elemento NullProcessing &#40;ASSL&#41; ](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl) a `Preserve` para las medidas de recuento distintivas.  Lamentablemente, esta práctica producía a menudo resultados no válidos y, a veces, incluso bloqueaba el trabajo de procesamiento. Como resultado, esta configuración ya no es válida en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Intentar usarla provocará el siguiente error de validación que se produzca: "Errores del Administrador de metadatos. Preserve no es un valor NullProcessing válido para el \<measurename > medida de recuento distintiva. "  
  
#### <a name="cube-browser-in-management-studio-and-cube-designer-has-been-removed"></a>Se ha quitado el explorador de cubos en Management Studio y el Diseñador de cubos  
 El control del explorador de cubos que permite arrastrar y colocar campos en una estructura de tabla dinámica en Management Studio o en el Diseñador de cubos se ha quitado del producto. El control era un componente de control Web de Office (OWC). OWC está en desuso en Office y ya no está disponible.  
  
### <a name="powerpivot-for-sharepoint"></a>PowerPivot para SharePoint  
  
#### <a name="higher-permission-requirements-for-using-a-powerpivot-workbook-as-an-external-data-source"></a>Mayores requisitos de permisos para utilizar un libro PowerPivot como origen de datos externo  
 Un libro de Excel puede representar los datos PowerPivot insertados en el mismo libro o en un libro externo. En la versión anterior, los requisitos de los permisos eran los mismos independientemente de si los datos PowerPivot estaban insertados o eran externos. Si únicamente tenía permisos de **Vista solo** en un libro PowerPivot, podía tener acceso total a todos los datos PowerPivot del libro para conexiones tanto insertadas como externas.  
  
 En esta versión, los requisitos de permisos han cambiado para los libros de Excel que representan los datos PowerPivot desde un archivo externo. En esta versión, debe tener permisos de **Lectura** (o más específicamente, el permiso para **Abrir elementos** ) para conectarse a un libro PowerPivot externo desde una aplicación cliente. Los permisos adicionales especifican que un usuario tiene derechos de descarga para ver los datos de origen insertados en el libro. Los permisos adicionales reflejan el hecho de que los datos del modelo estén totalmente disponibles para la aplicación cliente o el libro al que se vincula, por lo que se logra un mejor alineación entre los requisitos de los permisos y el comportamiento de conexión actual de los datos.  
  
 Para seguir utilizando un libro PowerPivot como origen de datos externo, debe aumentar los permisos de SharePoint para los usuarios que se conecten a los datos PowerPivot externos. Hasta que cambie los permisos, los usuarios obtendrán el siguiente error si intentan tener acceso a los libros PowerPivot en una conexión de origen de datos: "El servicio PowerPivot Web devolvió un error (acceso denegado. El documento solicitado no existe o no tiene permiso para abrir el archivo.)"  
  
> [!WARNING]  
>  Los pasos siguientes le dan instrucciones para anular la herencia de permisos en el nivel de la biblioteca y aumentar permisos de usuario **Solo ver** a **Lectura** para documentos concretos de esta biblioteca. Antes de continuar, revise cuidadosamente los permisos y los documentos existentes, y compruebe que estos pasos son adecuados para el sitio.  
>   
>  Como alternativa, puede crear una carpeta de la biblioteca, mover todos los documentos afectados a dicha carpeta y establecer permisos exclusivos en ella.  
  
> [!NOTE]  
>  Si los libros se almacenan en la Galería de PowerPivot, anular la herencia de permisos en un libro interrumpirá la generación de imágenes en miniatura para ese libro si está configurada para la actualización de datos. Para permitir simultáneamente el acceso tanto a los libros como a las imágenes de vista previa de la galería, considere conceder a usuarios específicos los permisos de **Lectura** en el nivel de la biblioteca, para todos los documentos de la biblioteca.  
  
 Debe ser propietario del sitio para cambiar los permisos.  
  
 **Cómo aumentar los permisos para leer el nivel de permiso de libros individuales**  
  
1.  Haga clic en la flecha hacia abajo para abrir el menú para un documento individual.  
  
2.  Haga clic en **Administrar permisos**.  
  
3.  De forma predeterminada, una biblioteca hereda los permisos. Para cambiar los permisos de libros individuales en esta biblioteca, haga clic en **Dejar de heredar permisos**.  
  
4.  Active la casilla según los nombres de usuario o de grupo que requieran permisos adicionales en los libros PowerPivot. Los permisos adicionales permitirán a estos usuarios vincularse a los datos PowerPivot incrustados y utilizar esos datos como origen de datos externo en otros documentos.  
  
5.  Haga clic en **Editar permisos de usuario**.  
  
6.  Elija los permisos de **Lectura** y haga clic en **Aceptar**.  
  
#### <a name="powerpivot-gallery-new-rules-for-snapshot-generation-for-some-powerpivot-workbooks"></a>Galería de PowerPivot: Nuevas reglas de generación de instantáneas para algunos libros PowerPivot  
 Esta versión presenta nuevos requisitos para generar imágenes de instantáneas en la Galería de PowerPivot, evitando la posible divulgación de información (a saber, mostrando una instantánea de los datos de un origen de datos que no tenga el permiso para ver). Estos requisitos se aplican solo a los libros PowerPivot que se conectan a orígenes de datos externos cada vez que se ve el libro. Si utiliza solo los libros que visualizan los datos PowerPivot incrustados, no verá ningún cambio en el modo en que las instantáneas se generan en la Galería de PowerPivot.  
  
 Para un libro que actualiza los datos cada vez que se abre, los nuevos requisitos para la generación de instantáneas son los siguientes:  
  
-   Los libros PowerPivot que otros libros o informes usan como orígenes de datos externos deben estar en la misma biblioteca que los libros que utilizan los datos. Por ejemplo, si el libro sales-data.xlsx proporciona datos al libro sales-report.xlsx, ambos deben estar en la galería para que las imágenes de instantáneas aparezcan.  
  
-   Los libros que se usan juntos deben heredar los permisos de un elemento primario común (es decir, la Galería de PowerPivot). En nuestro ejemplo, sales-data.xlsx y sales-report.xlsx deben heredar de la Galería de PowerPivot.  
  
 Si un libro no puede cumplir alguno de los criterios anteriores, el icono de bloqueado siguiente aparecerá en lugar de la imagen en miniatura esperada:  
  
 ![GMNI_PowerPivotGalleryIcon_Locked](media/gmni-powerpivotgalleryicon-locked.gif "GMNI_PowerPivotGalleryIcon_Locked")  
  
#### <a name="new-default-setting-for-load-balancing-requests-changed-from-round-robin-to-health-based"></a>La nueva configuración predeterminada de las solicitudes de equilibrio de carga ha pasado de realizarse con operación por turnos (Round-Robin) a basarse en el estado (Health-Based).  
 Una aplicación de servicio PowerPivot tiene una configuración predeterminada que determina cómo se distribuyen las solicitudes de datos PowerPivot a través de varios servidores PowerPivot para SharePoint en una granja. En la versión anterior, la configuración predeterminada era **Round Robin**, donde las solicitudes se distribuían de forma secuencial entre los servidores disponibles. En esta versión, el valor predeterminado es ahora **Basado en estado**. La aplicación de servicio PowerPivot utiliza las estadísticas de estado del servidor, como la memoria o CPU disponible, para determinar qué instancia de servidor obtiene la solicitud.  
  
 Si actualizó el servidor de la versión anterior, la aplicación de servicio PowerPivot mantiene la configuración predeterminada anterior (**Round Robin**). Para utilizar la configuración del método de asignación **Basado en estado** , debe modificarla. Para obtener más información, consulte [crear y configurar una aplicación de servicio PowerPivot en Administración Central](power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con versiones anteriores](../../2014/getting-started/backward-compatibility.md)   
 [Cambios importantes en Analysis Services las características de SQL Server 2014](breaking-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
  
