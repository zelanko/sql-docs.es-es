---
title: Actualizar libros y actualización de datos programada (SharePoint 2013) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a49c4af4-e243-4926-be97-74da1f9d54eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 57fe740bdd02c96eb21994f5996c734620793616
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079840"
---
# <a name="upgrade-workbooks-and-scheduled-data-refresh-sharepoint-2013"></a>Actualizar libros y actualización de datos programada (SharePoint 2013)
  En este tema se explica la experiencia de usuario de libros creados en entornos anteriores de PowerPivot y cómo actualizar los libros PowerPivot para poder aprovechar las nuevas características presentadas en esta versión. Para obtener más información acerca de las nuevas características, vea [novedades de PowerPivot](https://go.microsoft.com/fwlink/?LinkID=203917).  
  
> [!WARNING]  
>  No se puede revertir la actualización de los libros que se actualizan automáticamente en el servidor. Una vez actualizado un libro, permanece actualizado. Para usar una versión anterior, puede volver a publicar el libro anterior en SharePoint, restaurar una versión anterior o reciclar el libro. Para obtener más información acerca de cómo restaurar o reciclar un documento en SharePoint, vea [Planear la protección de contenido mediante papeleras de reciclaje y control de versiones](https://go.microsoft.com/fwlink/?LinkId=238669).  
  
 Este tema contiene las siguientes secciones:  
  
-   [Información general sobre la actualización de libros](#bkmk_overview)  
  
-   [Actualizar a SQL Server 2012 libros de Service Pack 1 (SP1) de libros de 2008 R2](#bkmk_to_2012sp1_from_2008r2)  
  
-   [Actualizar libros a Office 2013 desde versiones creadas con el complemento 2012 PowerPivot para Excel](#bkmk_to_2012sp1_from_2012)  
  
-   [Actualizar a libros de SQL Server 2012 desde versiones creadas con el complemento 2008 R2 PowerPivot para Excel 2010](#bkmk_to_2012_from_2008R2)  
  
-   [Ejecutar varias versiones de libro en un servidor más reciente](#bkmk_runold)  
  
##  <a name="bkmk_overview"></a>Información general sobre la actualización de libros  
 Un libro PowerPivot es un libro de Excel que contiene datos PowerPivot incrustados. Actualizar un libro tiene dos ventajas:  
  
-   Usar las nuevas características de [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)].  
  
-   Habilita la actualización de datos programada para los libros que se ejecutan con servidor de [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] Analysis Services en modo de SharePoint.  
  
> [!IMPORTANT]  
>  No puede revertir un libro actualizado, por lo que debe asegurarse de realizar una copia del archivo si desea usarlo en la versión anterior de [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]o en una versión anterior de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 En la tabla siguiente se muestran la compatibilidad y el comportamiento de los libros PowerPivot según el entorno en el que se creó el libro. El comportamiento descrito incluye la experiencia general del usuario, las opciones de actualización admitidas para actualizar el libro al entorno concreto y el comportamiento de la actualización de datos programada de un libro que aún no se ha actualizado.  
  
### <a name="workbook-behavior-and-upgrade-options"></a>Comportamiento y opciones de actualización del libro  
  
|Creado en|\<|Compatibilidad y comportamiento|>|  
|----------------|--------|--------------------------|--------|  
||**PowerPivot para SharePoint 2010 de 2008 R2**|**PowerPivot para SharePoint 2010 de 2012**|**PowerPivot para SharePoint 2013 de 2012 SP1**|  
|**2008 R2 PowerPivot para Excel 2010**|Todas las características|**Experiencia:** Los usuarios pueden interactuar con el libro en el explorador y usarlo como origen de datos para otras soluciones.<br /><br /> **Actualización:** Los libros se actualizarán automáticamente en la biblioteca de documentos si la actualización automática está habilitada para el servicio de sistema de PowerPivot en la granja de servidores de SharePoint.<br /><br /> **Programar la actualización de datos:** NO compatible. Es necesario actualizar el libro.|**Experiencia:** Los usuarios pueden interactuar con el libro y usarlo como origen de datos para otras soluciones.<br /><br /> **Actualización:** La actualización automática no está disponible. Los usuarios deben actualizar manualmente sus libros de 2008 R2 a la versión 2012 o a la versión de Office 2013.<br /><br /> **Programar la actualización de datos:** NO compatible. Es necesario actualizar el libro.|  
|**2012 PowerPivot para Excel**|No compatible|Todas las características|**Experiencia:** Los usuarios pueden interactuar con el libro en el explorador y usarlo como origen de datos para otras soluciones. La programación de la actualización de datos está disponible.<br /><br /> **Actualización:** No se admite la actualización automática. Los usuarios pueden actualizar manualmente sus libros a la versión de Office 2013.<br /><br /> **Programar actualización de datos:** se admite.|  
|**Excel 2013**|No compatible|No compatible|Todas las características|  
  
##  <a name="bkmk_to_2012sp1_from_2008r2"></a>Actualizar a SQL Server 2012 libros de Service Pack 1 (SP1) de libros de 2008 R2  
 En esta sección se describe cómo actualizar libros de SQL Server 2008 R2 PowerPivot para Excel 2010 a libros de SQL Server 2012 SP1 PowerPivot para Excel 2013.  
  
 **Cambio de comportamiento:** Los libros PowerPivot SQL Server 2008 R2 no se actualizarán automáticamente cuando se usen en SQL Server 2012 SP1 PowerPivot para SharePoint 2013. Por tanto, las actualizaciones de datos programadas no funcionarán para los libros de SQL Server 2008 R2 PowerPivot.  
  
 Los libros de SQL Server 2008 R2 se abrirán en PowerPivot para SharePoint 2013, pero las actualizaciones de datos programadas no funcionarán. Si examina el historial de actualización verá un mensaje de error similar al siguiente:  
  
 "El libro contiene un modelo de PowerPivot no admitido. El modelo de PowerPivot del libro tiene el formato de SQL Server 2008 R2 PowerPivot para Excel 2010. Los modelos de PowerPivot admitidos son los siguientes:  
  
-   SQL Server 2012 PowerPivot para Excel 2010.  
  
-   SQL Server 2012 PowerPivot para Excel 2013.  
  
 **Cómo actualizar un libro:** La actualización de datos programada no funcionará hasta que actualice el libro a un libro de 2012. Para actualizar el libro y el modelo que contiene, complete una de las acciones siguientes:  
  
-   Descargue y abra el libro en Microsoft Excel 2010 con el complemento SQL Server 2012 PowerPivot para Excel instalado.  
  
     Abra la ventana de PowerPivot y actualice el modelo de PowerPivot.  
  
     Después, guarde el libro y vuelva a publicarlo en SharePoint.  
  
-   Descargue y abra el libro en Microsoft Excel 2013.  
  
     Abra la ventana de PowerPivot y actualice el modelo de PowerPivot.  
  
     Después, guarde el libro y vuelva a publicarlo en el servidor de SharePoint.  
  
 Para obtener más información sobre los cambios en las características de Analysis Services, vea [cambios de comportamiento en Analysis Services características en SQL Server 2014](../../behavior-changes-to-analysis-services-features-in-sql-server-2014.md)  
  
 Para obtener más información sobre el historial de actualización, vea [ver el historial de actualización de datos &#40;PowerPivot para SharePoint&#41;](../../power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
##  <a name="bkmk_to_2012sp1_from_2012"></a>Actualizar a libros de Office 2013 desde versiones creadas con 2012 el complemento de PowerPivot para Excel  
 En esta sección se describe cómo actualizar libros **de** SQL Server 2012 PowerPivot para Excel 2010 **a** SQL Server 2012 SP1 PowerPivot para Excel 2013.  
  
 La actualización de un libro resuelve el siguiente error que aparece al intentar la actualización de datos programada en el libro de una versión anterior:  
  
 "La operación de actualización de los libros creados con la versión anterior de PowerPivot no está disponible".  
  
 **Cómo actualizar un libro**  
  
1.  Actualice cada libro manualmente abriéndolo en Microsoft Excel 2013.  
  
2.  Para actualizar el libro y el modelo que contiene, descargue y abra el libro en Microsoft Excel 2013.  
  
3.  Abra la ventana de PowerPivot y actualice el modelo de PowerPivot.  
  
4.  Después, guarde el libro y vuelva a publicarlo en el servidor de SharePoint 2013.  
  
##  <a name="bkmk_to_2012_from_2008R2"></a>Actualización de los libros de SQL Server 2012 a partir de las versiones creadas con el complemento 2008 R2 PowerPivot para Excel 2010  
 En esta sección se describe cómo actualizar libros **de** SQL Server 2008 R2 PowerPivot para Excel 2010 **a** libros de SQL Server 2012 PowerPivot para Excel 2010.  
  
 La actualización de un libro resuelve el siguiente error que aparece al intentar la actualización de datos programada en el libro de una versión anterior:  
  
 "La operación de actualización de los libros creados con la versión anterior de PowerPivot no está disponible".  
  
 **Cómo actualizar un libro**  
  
 Hay dos formas de realizar la actualización:  
  
1.  Actualice cada libro manualmente; para ello, ábralo en Excel en un equipo que tenga la versión [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] de PowerPivot para Excel y, a continuación, vuelva a publicarlo en el servidor. Al abrir el libro en la versión más reciente del complemento, se producen las operaciones internas siguientes: el proveedor de datos en la cadena de conexión de datos del libro se actualiza a MSOLAP.5, se actualizan los metadatos y las relaciones se vuelven a crear para adecuarlas a una implementación más reciente.  
  
2.  Como alternativa, un administrador de SharePoint puede permitir que la característica de actualización automática para el servicio del sistema PowerPivot de una granja de servidores de SharePoint actualice automáticamente un libro de [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] PowerPivot cuando se ejecute la actualización de datos programada (solo se actualizan los libros que están configurados para la actualización de datos programada).  
  
    > [!NOTE]  
    >  La actualización automática es una característica de configuración del servidor; no puede habilitarla o deshabilitarla para libros, bibliotecas o colecciones de sitios concretos.  
  
 **Cómo configurar la actualización automática durante la actualización de datos**  
  
 Para usar la actualización automática, debe activar la casilla **Actualizar automáticamente los libros PowerPivot para habilitar la actualización de datos desde el servidor** en la herramienta de configuración de PowerPivot. En la herramienta, la casilla está en la página **Actualizar el servicio de sistema de PowerPivot** y en la página **Crear una aplicación de servicio PowerPivot** si se configura una nueva instalación.  
  
 Puede ejecutar el cmdlet siguiente para comprobar si la actualización automática está habilitada:  
  
```  
PS C:\Windows\system32> Get-PowerPivotSystemService  
```  
  
 La salida de Get-PowerPivotSystemService es una lista de propiedades y valores correspondientes. Debería aparecer `WorkbookUpgradeOnDataRefresh` en la lista de propiedades. Se establecerá en **true** si la actualización automática está habilitada. Si es **false**, continúe en el paso siguiente, habilitar la actualización automática del libro.  
  
 Para habilitar la actualización automática del libro, ejecute el comando siguiente:  
  
```  
PS C:\Windows\system32> Set-PowerPivotSystemService -WorkbookUpgradeOnDataRefresh:$true -Confirm:$false  
```  
  
 Después de actualizar el libro, puede usar la actualización de datos programada y las nuevas características del complemento PowerPivot para Excel.  
  
##  <a name="bkmk_runold"></a>Ejecutar varias versiones de libro en un servidor más reciente  
 Puede ejecutar versiones anteriores y recientes de los libros PowerPivot en paralelo en una instancia de [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].  
  
 Según cómo haya instalado el servidor, **es posible que necesite** instalar una versión anterior del proveedor OLE DB de Analysis Services para poder obtener acceso a libros anteriores y recientes en el mismo servidor.  
  
 Tenga en cuenta que no se admite la publicación de libros de una versión más reciente en instancias anteriores de SQL Server de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] . Una instancia de [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] no cargará un libro creado en la versión de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] de [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)]y una instancia de SQL Server 2012 no cargará libros de Office 2013 con modelos de datos avanzados que se hayan creado con la versión de [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)] de PowerPivot en Excel.  
  
###  <a name="bkmk_msolapxslx"></a>Cómo comprobar la información del proveedor de datos MSOLAP en un libro PowerPivot  
 Siga estas indicaciones para comprobar qué proveedor OLE DB se utiliza en un libro PowerPivot. La comprobación de la información de conexión de datos no requiere que se instale el complemento de [!INCLUDE[ssGeminiClient](../../../includes/ssgeminiclient-md.md)] .  
  
1.  En Excel, en la pestaña Datos, haga clic en **Conexiones**. Haga clic en **Propiedades**.  
  
2.  En la pestaña **Definición** , la versión del proveedor aparece al principio de la cadena de conexión.  
  
     **Provider = msolap. 5** indica que el [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]libro es.  
  
     **Provider = msolap. 4** indica [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)].  
  
     **Data Source = $Embedded $** indica que el libro es un libro PowerPivot, con una base de datos incrustada.  
  
###  <a name="bkmk_msolappc"></a>Cómo comprobar la versión actual del proveedor de datos MSOLAP en un equipo local  
 Utilice las siguientes instrucciones para comprobar qué proveedor OLE DB es la versión actual en el servidor o la estación de trabajo que ejecuta los libros PowerPivot. Conocer la versión actual puede ayudarle a solucionar errores de conexión de los datos después de actualizar.  
  
1.  En el Editor del Registro, vaya a HKEY_CLASSES_ROOT  
  
2.  Desplácese hasta MSOLAP. Compruebe que MSOLAP.5 aparece entre los proveedores OLAP instalados en el sistema. Compruebe que MSOLAP | CurVer está establecido en MSOLAP.5  
  
## <a name="see-also"></a>Consulte también  
 [Migrar PowerPivot a SharePoint 2013](migrate-power-pivot-to-sharepoint-2013.md)   
 [PowerPivot para SharePoint de actualización](../../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
 [Novedades de Analysis Services y Business Intelligence](../../what-s-new-in-analysis-services.md)   
 [Ver el historial de actualización de datos &#40;PowerPivot para SharePoint&#41;](../../power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md)  
  
  
