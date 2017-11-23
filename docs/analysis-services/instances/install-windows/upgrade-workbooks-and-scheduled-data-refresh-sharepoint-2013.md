---
title: "Actualizar libros y actualización de datos programada (SharePoint 2013) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: instances
ms.reviewer: 
ms.suite: sql
ms.technology: setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a49c4af4-e243-4926-be97-74da1f9d54eb
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ffec3fb3ec6abd9d6fd1779ae8e8f434894e68b9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>Actualizar libros y actualización de datos programada (SharePoint 2013)
  En este tema se explica la experiencia de usuario de libros creados en entornos anteriores de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y cómo actualizar los libros de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para poder aprovechar las nuevas características presentadas en esta versión. Para obtener más información sobre las nuevas características, vea [Novedades de Power Pivot](http://go.microsoft.com/fwlink/?LinkID=203917).  
  
> [!WARNING]  
>  No se puede revertir la actualización de los libros que se actualizan automáticamente en el servidor. Una vez actualizado un libro, permanece actualizado. Para usar una versión anterior, puede volver a publicar el libro anterior en SharePoint, restaurar una versión anterior o reciclar el libro. Para obtener más información acerca de cómo restaurar o reciclar un documento en SharePoint, vea [Planear la protección de contenido mediante papeleras de reciclaje y control de versiones](http://go.microsoft.com/fwlink/?LinkId=238669).  
  
 Este tema contiene las siguientes secciones:  
  
-   [Información general sobre la actualización de libros](#bkmk_overview)  
  
-   [Actualizar libros de SQL Server 2008 R2 a libros de SQL Server 2012 Service Pack 1 (SP1)](#bkmk_to_2012sp1_from_2008r2)  
  
-   [Actualizar libros a Office 2013 desde versiones creadas con el complemento 2012 Power Pivot para Excel](#bkmk_to_2012sp1_from_2012)  
  
-   [Actualizar a libros de SQL Server 2012 desde versiones creadas con el complemento 2008 R2 Power Pivot para Excel 2010](#bkmk_to_2012_from_2008R2)  
  
-   [Ejecutar varias versiones de un libro en un servidor más reciente](#bkmk_runold)  
  
##  <a name="bkmk_overview"></a> Información general sobre la actualización de libros  
 Un libro de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] es un libro de Excel que contiene los datos incrustados de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Actualizar un libro tiene dos ventajas:  
  
-   Usar las nuevas características de [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)].  
  
-   Habilita la actualización de datos programada para los libros que se ejecutan con servidor de [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] Analysis Services en modo de SharePoint.  
  
> [!IMPORTANT]  
>  No puede revertir un libro actualizado, por lo que debe asegurarse de realizar una copia del archivo si desea usarlo en la versión anterior de [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]o en una versión anterior de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 En la tabla siguiente se muestran la compatibilidad y el comportamiento de los libros de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] según el entorno en el que se creó el libro. El comportamiento descrito incluye la experiencia general del usuario, las opciones de actualización admitidas para actualizar el libro al entorno concreto y el comportamiento de la actualización de datos programada de un libro que aún no se ha actualizado.  
  
### <a name="workbook-behavior-and-upgrade-options"></a>Comportamiento y opciones de actualización del libro  
  
|Creado en|\<|Compatibilidad y comportamiento|>|  
|----------------|--------|--------------------------|--------|  
||**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2010**|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2010**|**2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013**|  
|**2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010**|Todas las características|**Experiencia** : los usuarios pueden interactuar con el libro en el explorador y usarlo como origen de datos para otras soluciones.<br /><br /> **Actualización** : los libros se actualizarán automáticamente en la biblioteca de documentos si la actualización automática está habilitada para el servicio del sistema de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en la granja de servidores de SharePoint.<br /><br /> **Programar la actualización de datos** : NO se admite. Es necesario actualizar el libro.|**Experiencia** : los usuarios pueden interactuar con el libro y usarlo como origen de datos para otras soluciones.<br /><br /> **Actualización** : la actualización automática no está disponible. Los usuarios deben actualizar manualmente sus libros de 2008 R2 a la versión 2012 o a la versión de Office 2013.<br /><br /> **Programar la actualización de datos** : NO se admite. Es necesario actualizar el libro.|  
|**2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel**|No compatible|Todas las características|**Experiencia** : los usuarios pueden interactuar con el libro en el explorador y usarlo como origen de datos para otras soluciones. La programación de la actualización de datos está disponible.<br /><br /> **Actualización** : la actualización automática no se admite. Los usuarios pueden actualizar manualmente sus libros a la versión de Office 2013.<br /><br /> **Programar la actualización de datos** : se admite.|  
|**Excel 2013**|No compatible|No compatible|Todas las características|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a> Actualizar libros de SQL Server 2008 R2 a libros de SQL Server 2012 Service Pack 1 (SP1)  
 En esta sección se describe cómo actualizar libros de SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010 a libros de SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2013.  
  
 **Cambio de comportamiento** : los libros de SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no se actualizarán automáticamente cuando se usen en SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013. Por tanto, las actualizaciones de datos programadas no funcionarán para los libros de SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]  
  
 Los libros de SQL Server 2008 R2 se abrirán en [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para SharePoint 2013, pero las actualizaciones de datos programadas no funcionarán. Si examina el historial de actualización verá un mensaje de error similar al siguiente:  
  
 “El libro contiene un modelo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no admitido”. El modelo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] del libro tiene el formato de SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010. Los modelos de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] admitidos son los siguientes:  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010.  
  
-   SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2013.  
  
 **Cómo actualizar un libro** : la actualización de datos programada no funcionará hasta que actualice el libro a un libro de 2012. Para actualizar el libro y el modelo que contiene, complete una de las acciones siguientes:  
  
-   Descargue y abra el libro en Microsoft Excel 2010 con el complemento SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel instalado.  
  
     Abra la ventana [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y actualice el modelo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     Después, guarde el libro y vuelva a publicarlo en SharePoint.  
  
-   Descargue y abra el libro en Microsoft Excel 2013.  
  
     Abra la ventana [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y actualice el modelo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
     Después, guarde el libro y vuelva a publicarlo en el servidor de SharePoint.  
  
 Para obtener más información sobre los cambios realizados en las características de Analysis Services, vea [Cambios de comportamiento en las características de Analysis Services en SQL Server 2016](../../../analysis-services/behavior-changes-to-analysis-services-features-in-sql-server-2016.md).  
  
 Para obtener más información sobre el historial de actualización, vea [Ver el Historial de actualización de datos &#40;Power Pivot para SharePoint&#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a> Actualizar libros a Office 2013 desde versiones creadas con el complemento 2012 Power Pivot para Excel  
 En esta sección se describe cómo actualizar libros **de** SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010 **a** SQL Server 2012 SP1 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2013.  
  
 La actualización de un libro resuelve el siguiente error que aparece al intentar la actualización de datos programada en el libro de una versión anterior:  
  
 "No está disponible la operación de actualización de libros creada con una versión anterior de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ".  
  
 **Cómo actualizar un libro**  
  
1.  Actualice cada libro manualmente abriéndolo en Microsoft Excel 2013.  
  
2.  Para actualizar el libro y el modelo que contiene, descargue y abra el libro en Microsoft Excel 2013.  
  
3.  Abra la ventana [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] y actualice el modelo de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] .  
  
4.  Después, guarde el libro y vuelva a publicarlo en el servidor de SharePoint 2013.  
  
##  <a name="bkmk_to_2012_from_2008R2"></a> Actualizar a libros de SQL Server 2012 desde versiones creadas con el complemento 2008 R2 Power Pivot para Excel 2010  
 En esta sección se describe cómo actualizar libros **de** SQL Server 2008 R2 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010 **a** SQL Server 2012 [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel 2010.  
  
 La actualización de un libro resuelve el siguiente error que aparece al intentar la actualización de datos programada en el libro de una versión anterior:  
  
 "No está disponible la operación de actualización de libros creada con una versión anterior de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] ".  
  
 **Cómo actualizar un libro**  
  
 Hay dos formas de realizar la actualización:  
  
1.  Actualice cada libro manualmente; para ello, ábralo en Excel en un equipo que tenga la versión [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel y luego vuelva a publicarlo en el servidor. Al abrir el libro en la versión más reciente del complemento, se producen las operaciones internas siguientes: el proveedor de datos en la cadena de conexión de datos del libro se actualiza a MSOLAP.5, se actualizan los metadatos y las relaciones se vuelven a crear para adecuarlas a una implementación más reciente.  
  
2.  Como alternativa, un administrador de SharePoint puede permitir que la característica de actualización automática para el Servicio de sistema de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] de una granja de servidores de SharePoint actualice automáticamente un libro de [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)][!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] cuando se ejecute la actualización de datos programada (solo se actualizan los libros que están configurados para la actualización de datos programada).  
  
    > [!NOTE]  
    >  La actualización automática es una característica de configuración del servidor; no puede habilitarla o deshabilitarla para libros, bibliotecas o colecciones de sitios concretos.  
  
 **Cómo configurar la actualización automática durante la actualización de datos**  
  
 Para usar la actualización automática, debe activar la casilla **Actualizar automáticamente los libros de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para habilitar la actualización de datos desde el servidor** en la herramienta de configuración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]. En la herramienta, la casilla está en la página **Actualizar el servicio de sistema de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]** y en la página **Crear una aplicación de servicio de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]** si se configura una nueva instalación.  
  
 Puede ejecutar el cmdlet siguiente para comprobar si la actualización automática está habilitada:  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 La salida de Get-PowerPivotSystemService es una lista de propiedades y valores correspondientes. Debería aparecer **WorkbookUpgradeOnDataRefresh** en la lista de propiedades. Se establecerá en **true** si la actualización automática está habilitada. Si es **false**, continúe en el paso siguiente, habilitar la actualización automática del libro.  
  
 Para habilitar la actualización automática del libro, ejecute el comando siguiente:  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService –WorkbookUpgradeOnDataRefresh:$true –Confirm:$false  
```  
  
 Después de actualizar el libro, puede usar la actualización de datos programada y las nuevas características del complemento [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para Excel.  
  
##  <a name="bkmk_runold"></a> Ejecutar varias versiones de un libro en un servidor más reciente  
 Puede ejecutar versiones anteriores y recientes de los libros de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en paralelo en una instancia de [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 Según cómo haya instalado el servidor, **es posible que necesite** instalar una versión anterior del proveedor OLE DB de Analysis Services para poder obtener acceso a libros anteriores y recientes en el mismo servidor.  
  
 Tenga en cuenta que no se admite la publicación de libros de una versión más reciente en instancias anteriores de SQL Server de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] . Una instancia de [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] no cargará un libro creado en la versión de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] de [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]y una instancia de SQL Server 2012 no cargará libros de Office 2013 con modelos de datos avanzados que se hayan creado con la versión de [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] en Excel.  
  
###  <a name="bkmk_msolapxslx"></a> Comprobar la información de proveedor de datos de MSOLAP en un libro de Power Pivot  
 Siga estas indicaciones para comprobar qué proveedor OLE DB se usa en un libro de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . La comprobación de la información de conexión de datos no requiere que se instale el complemento de [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] .  
  
1.  En Excel, en la pestaña Datos, haga clic en **Conexiones**. Haga clic en **Propiedades**.  
  
2.  En la pestaña **Definición** , la versión del proveedor aparece al principio de la cadena de conexión.  
  
     **Provider=MSOLAP.5** indica que el libro es [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
     **Provider=MSOLAP.4** indica [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)].  
  
     **Data Source=$Embedded$** indica que es un libro de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] , con una base de datos incrustada.  
  
###  <a name="bkmk_msolappc"></a> Comprobar la versión actual del proveedor de datos MSOLAP en un equipo local  
 Use las siguientes instrucciones para comprobar qué proveedor OLE DB es la versión actual en el servidor o la estación de trabajo que ejecuta los libros de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Conocer la versión actual puede ayudarle a solucionar errores de conexión de los datos después de actualizar.  
  
1.  En el Editor del Registro, vaya a HKEY_CLASSES_ROOT  
  
2.  Desplácese hasta MSOLAP. Compruebe que MSOLAP.5 aparece entre los proveedores OLAP instalados en el sistema. Compruebe que MSOLAP | CurVer está establecido en MSOLAP.5  
  
## <a name="see-also"></a>Vea también  
 [Migrar Power Pivot a SharePoint 2013](../../../analysis-services/instances/install-windows/migrate-power-pivot-to-sharepoint-2013.md)   
 [Actualización de PowerPivot para SharePoint](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Novedades de Analysis Services](../../../analysis-services/what-s-new-in-analysis-services.md)   
 [La actualización de datos de la vista Historial &#40; PowerPivot para SharePoint &#41;](../../../analysis-services/power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
