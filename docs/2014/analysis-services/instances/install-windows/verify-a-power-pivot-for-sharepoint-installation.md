---
title: Verify a PowerPivot para SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 855bd055-5ad3-493f-9c5b-1f5297b2e6e2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c4ce1b1485885719bcd31cb085d43379239612d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66079866"
---
# <a name="verify-a-powerpivot-for-sharepoint-installation"></a>Comprobar una instalación de PowerPivot para SharePoint
  Una instancia de PowerPivot para SharePoint que instale en una granja de servidores de SharePoint se administra a través de Administración central de SharePoint. Como mínimo, puede comprobar las páginas de Administración central y de sitios de SharePoint para comprobar que están disponibles los componentes de servidor y las características de PowerPivot. Sin embargo, para comprobar una instalación por completo, debe tener un libro PowerPivot que pueda publicar en SharePoint y al que pueda tener acceso desde una biblioteca. Para realizar la prueba, puede publicar un libro de ejemplo que contenga datos PowerPivot y usarlo para confirmar que la integración de SharePoint está configurada correctamente.  
  
##  <a name="verifyinstall"></a> Comprobar la integración de Administración central  
 Para comprobar la integración de PowerPivot con Administración central, haga lo siguiente:  
  
1.  En el menú Inicio, haga clic en **todos los programas**, abra productos de Microsoft SharePoint 2010 y haga clic en **SharePoint 2010 Central Administration**.  
  
2.  Escriba su nombre de usuario y contraseña, y a continuación haga clic en **Aceptar**.  
  
     Si lo desea, puede modificar la configuración del explorador para no tener que escribir un nombre de usuario y una contraseña cada vez que abra Administración central. Para agregar la Administración central como un sitio de confianza, haga lo siguiente.  
  
    1.  En Internet Explorer, en el menú Herramientas, haga clic en **Opciones de Internet**.  
  
    2.  En la pestaña Seguridad, en la sección **Seleccione una zona para ver o cambiar la configuración de seguridad** , haga clic en Sitios de confianza y, a continuación, haga clic en Sitios.  
  
    3.  Desactive la casilla **Requerir comprobación del servidor (https:) para todos los sitios de esta zona** .  
  
    4.  En **Agregar este sitio web a la zona**, escriba la dirección URL a su sitio y, a continuación, haga clic en **Agregar**.  
  
    5.  Haga clic en **Cerrar**y, a continuación, en **Aceptar**.  
  
        > [!NOTE]  
        >  La documentación de la instalación de SharePoint incluye instrucciones adicionales para trabajar con los errores del servidor proxy y deshabilitar la Configuración de seguridad mejorada de Internet Explorer para poder descargar e instalar las actualizaciones. Para obtener más información, vea la sección **Realizar tareas adicionales** en [Implementar un único servidor con SQL Server](https://go.microsoft.com/fwlink/?LinkId=177754) en el sitio web de Microsoft.  
  
3.  En Administración central, en Configuración del sistema, haga clic en **Administrar características de la granja**.  
  
4.  Compruebe que la **Característica de integración de PowerPivot** está **Activa**.  
  
5.  En Administración central, en Configuración del sistema, haga clic en **Administrar servicios en el servidor**.  
  
6.  Compruebe que se hayan iniciado **SQL Server Analysis Services** y **Servicio de sistema de SQL Server PowerPivot** .  
  
7.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
8.  Haga clic en **aplicación de servicio PowerPivot predeterminada** para abrir el panel de administración de PowerPivot para esta aplicación. Al usarse por primera vez, el panel tarda varios minutos en cargarse.  
  
     Como alternativa, haga clic en el espacio vacío junto a **aplicación de servicio PowerPivot predeterminada** para seleccionar la fila y haga clic en **propiedades** para ver las opciones de configuración para esta aplicación de servicio. Puede modificar la configuración y las propiedades de aplicación para cambiar la configuración del servidor. Para obtener más información sobre estas opciones, consulte [crear y configurar una aplicación de servicio PowerPivot en Administración Central](../../power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
## <a name="verify-integration-at-the-site-level"></a>Comprobar la integración en el nivel de sitio  
 Para comprobar la integración de PowerPivot con un sitio de SharePoint, haga lo siguiente:  
  
1.  En un explorador, abra la aplicación web que ha creado. Si usa los valores predeterminados, puede especificar http://\<el nombre del equipo > en la dirección URL.  
  
2.  Compruebe que el acceso a datos y las características de procesamiento de PowerPivot están disponibles en la aplicación. Para ello, compruebe la presencia de plantillas de biblioteca proporcionadas por PowerPivot:  
  
    1.  En acciones del sitio, haga clic en **más opciones...** .  
  
    2.  En las bibliotecas, debería ver **biblioteca de fuentes de datos** y **Galería de PowerPivot**. La característica PowerPivot proporciona estas plantillas de biblioteca, que estarán visibles en la lista Bibliotecas si la característica está integrada correctamente.  
  
## <a name="verify-data-access-on-the-server"></a>Comprobar el acceso a datos en el servidor  
 Para comprobar el acceso a datos PowerPivot en el servidor, haga lo siguiente:  
  
1.  [Descargue](https://go.microsoft.com/fwlink/?LinkID=219108) el ejemplo de datos Picnic que acompaña a un tutorial de Reporting Services. Utilizará el libro de ejemplo de esta descarga para comprobar el acceso a datos PowerPivot. Extraiga los archivos.  
  
2.  Cargue el libro de Excel (.xlsx) en Documentos compartidos. El libro contiene los datos PowerPivot incrustados.  
  
3.  Haga clic en el documento para abrirlo desde la biblioteca.  
  
4.  Haga clic en una segmentación de datos o en un filtro en la parte superior del libro. Mes, color y tipo son segmentaciones de datos en este libro. Al hacer clic en una segmentación de datos, se inicia una consulta PowerPivot que demuestra que el servidor está operativo. El servidor cargará los datos PowerPivot en segundo plano y devolverá los resultados.  
  
5.  Vuelva a la biblioteca. Seleccione la flecha desplegable a la derecha del libro y, a continuación, haga clic en **Iniciar Power View**. Este paso confirma que la característica [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] de Reporting Services está operativa. Si no instaló Reporting Services, omita este paso.  
  
     En el paso siguiente, se conectará al servidor en Management Studio para comprobar que los datos se cargan y se almacenan en caché.  
  
6.  Inicie SQL Server Management Studio desde el grupo de programas [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] en el menú Inicio. Si esta herramienta no está instalada en el servidor, puede pasar al último paso para confirmar la presencia de archivos almacenados en caché.  
  
7.  En Tipo de servidor, seleccione **Analysis Services**.  
  
8.  En el nombre del servidor, escriba  **\<nombre del servidor > \powerpivot**, donde  **\<server-name >** es el nombre del equipo que tiene la instalación de PowerPivot para SharePoint.  
  
9. Haga clic en **Conectar**. De este modo se comprueba que el servidor de Analysis Services está disponible.  
  
10. En el Explorador de objetos, puede hacer clic en **bases de datos** para ver la lista de archivos de datos de PowerPivot que se cargan.  
  
11. En el sistema de archivos del equipo, compruebe la siguiente carpeta para determinar si hay archivos almacenados en la memoria caché del disco. La presencia de archivos almacenados en caché es una prueba más de que la implementación está operativa. Para ver la memoria caché de archivos, vaya a la \<unidad >: \Program Files\Microsoft SQL Server\MSAS11. Carpeta de aplicación de servicio PowerPivot POWERPIVOT\OLAP\Backup\Sandboxes\Default. Cada base de datos de la memoria caché está almacenada en su propia carpeta, con una convención de nomenclatura basada en GUID para asegurarse de que tiene un nombre único.  
  
  
