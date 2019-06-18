---
title: Usar una Conexión de datos de Office (.odc) con informes | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- Office Data Connection (.odc) files
- SharePoint integration [Reporting Services], shared data sources
- .odc files
ms.assetid: e8d6896d-f886-4390-8b5d-96f0a50c250c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a33b5bae668835ca1dbf52b2e7852c3af731ddfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574947"
---
# <a name="use-an-office-data-connection-odc-with-reports"></a>Usar una Conexión de datos de Office (.odc) con informes
  En escenarios limitados, puede usar un archivo de conexión de datos de Office (.odc) existente para proporcionar información de conexión a un informe de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Al crear un origen de datos compartido, puede usarse un archivo .odc en lugar de un archivo .rsds. El servidor de informes usa un archivo .odc de la misma forma que usa un archivo .rsds; lee el archivo para el tipo de origen de datos, una cadena de conexión y la información de credenciales.  
  
 No todos los archivos .odc pueden utilizarse con un informe de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La extensión de procesamiento de datos y las características del informe y del archivo .odc determinan si puede usarse un archivo .odc:  
  
-   El informe debe estar diseñado para funcionar con un proveedor de datos OLE DB u ODBC. Si ha usado una extensión de procesamiento de datos distinta para crear el informe, es posible que el informe o sus consultas incluyan funcionalidad que no sea compatible con el proveedor de datos OLE DB u ODBC.  
  
-   El archivo .odc debe tener la estructura y los elementos esperados. La configuración de proveedor de datos y de credenciales debe establecerse de forma explícita en el archivo para que el servidor de informes pueda leerla. La mejor forma de establecer estos valores es exportar el archivo .odc antes de cargarlo en la biblioteca de SharePoint.  
  
-   El archivo .odc debe especificar un tipo de conexión OLE DB u ODBC.  
  
-   El archivo .odc debe especificar una cadena de conexión.  
  
-   Las credenciales se pueden establecer en **None**, **Stored**o **Integrated**. Si el método de credenciales se establece en **Stored**, el servidor de informes solicitará al usuario las credenciales en lugar de usar las credenciales almacenadas. El servidor de informes no puede usar credenciales almacenadas, tal y como se define en el archivo .odc.  
  
-   El origen de datos debe tener un esquema idéntico al utilizado para crear el informe. Si las estructuras de datos son distintas, no se ejecutará el informe.  
  
-   El archivo .odc se debe crear en [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 2007 (las versiones anteriores de .odc no son compatibles con archivos de definición de informe).  
  
 No puede utilizar archivos .odc que especifiquen conexiones a orígenes de datos que no puedan procesarse en un servidor de informes, aunque los tipos de orígenes de datos .odc presenten un aspecto similar al de los tipos de orígenes de datos compatibles. Concretamente, si ha creado un archivo .odc en Microsoft Excel 2007 que recupera datos de Microsoft Access, Internet o un archivo de texto, no podrá usar el archivo .odc para proporcionar datos a un informe.  
  
 Los modelos e informes del Generador de informes no funcionan con archivos .odc. No puede utilizar un archivo .odc para crear un modelo y no puede configurar el modelo para utilizar un origen de datos compartido que se vincule a un archivo .odc.  
  
 Si no está familiarizado con los archivos .odc, puede usar las siguientes instrucciones para crear y exportar uno. Una forma fácil de crear un archivo .odc para un origen de datos OLE DB es usar Excel 2007 y el Asistente para la conexión de datos. Tenga en cuenta que el asistente no crea un origen de datos; debe tener un origen de datos externo que ya esté definido.  
  
 Un archivo .odc existente solo debería utilizarse si es totalmente compatible con el informe y las consultas. Si se producen errores que exigen modificaciones importantes del informe o archivo .odc, debe crear un nuevo archivo .rsds para el informe. Para más información sobre cómo crear un origen de datos compartido que use un archivo .rsds, vea [Crear y administrar orígenes de datos compartidos &#40;Reporting Services en el modo integrado de SharePoint&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
### <a name="to-create-and-export-an-odc-file"></a>Para crear y exportar un archivo .odc  
  
1.  Inicie Excel 2007.  
  
2.  En la pestaña **Datos** , en el grupo **Obtener datos externos** , haga clic en **Desde otras fuentes**y, a continuación, haga clic en **Desde el Asistente para la conexión de datos**.  
  
3.  Seleccione **Otro o avanzado**y, después, haga clic en **Siguiente**.  
  
4.  Seleccione **Proveedor Microsoft OLE DB para SQL Server**y, a continuación, haga clic en **Siguiente**.  
  
5.  Escriba el nombre del servidor (de forma predeterminada, es el nombre de red del equipo) y una cuenta de usuario que tenga permisos de base de datos e inicio de sesión válidos. Haga clic en **Siguiente**.  
  
6.  Seleccione una base de datos y, a continuación, haga clic en **Aceptar** para cerrar el cuadro de diálogo **Vínculo de datos** .  
  
7.  La casilla **Conectar con una tabla específica** está activada de forma predeterminada. Se usa para recuperar datos de una tabla específica. El servidor de informes omite todas las consultas de un archivo .odc, por lo que no importa si activa o desactiva la casilla. Las consultas que recuperan datos para un informe se incluyen en un archivo de definición de informe, no en archivos externos.  
  
8.  Mientras la conexión permanezca abierta, podrá modificar sus propiedades y exportarlo. En la pestaña **Datos** , en el grupo **Conexiones** , haga clic en **Propiedades**y, a continuación, haga clic en el botón **Propiedades de conexión** situado junto al nombre de conexión.  
  
9. En la pestaña **Definición** , haga clic en **Exportar archivo de conexión**.  
  
10. Escriba un nombre para el archivo y haga clic en **Guardar**. Cierre la aplicación y todos los archivos abiertos.  
  
### <a name="to-upload-and-use-an-odc-file"></a>Para cargar y usar un archivo .odc  
  
1.  Abra la biblioteca en la que desee cargar el archivo de conexión.  
  
2.  En el menú **Cargar** , haga clic en **Cargar documento**.  
  
3.  Haga clic en **Examinar**.  
  
4.  Seleccione el archivo .odc que ha creado. De forma predeterminada, el archivo .odc se guarda en la carpeta Mis documentos, en Mis archivos de origen de datos.  
  
5.  Haga clic en **Abrir** para seleccionar el archivo y haga clic en **Aceptar** para guardar la selección. La página de propiedades del nuevo elemento se abre automáticamente.  
  
6.  En Tipo de contenido, seleccione **Origen de datos de informe**y, a continuación, haga clic en **Aceptar**.  
  
7.  Seleccione un informe.  
  
8.  Haga clic en la flecha abajo y, a continuación, seleccione **Administrar orígenes de datos**.  
  
9. Haga clic en el nombre del origen de datos.  
  
10. Si el informe utiliza información de orígenes de datos personalizados, haga clic en **Compartido**.  
  
11. En **Vínculo a origen de datos**, haga clic en el botón para examinar ( **…** ).  
  
12. Seleccione el archivo .odc recién cargado.  
  
13. Haga clic en **Aceptar** para seleccionar el archivo y, a continuación, haga clic en **Aceptar** para guardar los cambios.  
  
     Si intenta seguir estos pasos con la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y los informes de ejemplo, tenga en cuenta que solo funcionará el informe Company Sales en un archivo .odc. Los otros informes de ejemplo contienen parámetros de consulta y características que no funcionan con el proveedor OLE DB. Sin embargo, puede hacer que los informes funcionen con el proveedor OLE DB modificándolos primero en el Diseñador de informes.  
  
## <a name="see-also"></a>Consulte también  
 [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)  
  
  
