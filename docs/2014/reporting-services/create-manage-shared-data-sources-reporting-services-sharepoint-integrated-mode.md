---
title: Crear y administrar orígenes de datos compartidos (Reporting Services en modo integrado de SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], shared data sources
- shared data sources [Reporting Services]
ms.assetid: 2d3428e4-a810-4e66-a287-ff18e57fad76
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5eedb74dd5a24f40469b3ee6a4a24e97e6e59174
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109630"
---
# <a name="create-and-manage-shared-data-sources-reporting-services-in-sharepoint-integrated-mode"></a>Crear y administrar orígenes de datos compartidos (Reporting Services en el modo integrado de SharePoint)
  Al ejecutar un informe desde una biblioteca de SharePoint, la información de conexión puede definirse dentro del informe o en un archivo externo que esté vinculado al informe. Si la información de conexión está incrustada en el informe, se denomina origen de datos personalizado. Si la información de conexión se define en un archivo externo, se denomina origen de datos compartido. El archivo externo puede ser un archivo de origen de datos del servidor de informes (.rsds) o un archivo de conexión de datos de Office (.odc).  
  
 Un archivo .rsds es similar a un archivo .rds, pero tiene un esquema distinto. Para crear un archivo .rsds, puede publicar un archivo .rds del Diseñador de informes o del Diseñador de modelos en una biblioteca de SharePoint (se creará un nuevo archivo .rsds a partir del archivo .rds original). O bien, puede crear un nuevo archivo en una biblioteca de un sitio de SharePoint.  
  
 Después de crear o publicar un origen de datos compartido, podrá editar las propiedades de conexión o eliminar el archivo si deja de usarse. Antes de eliminar un origen de datos compartido, debe determinar si lo usan los informes y modelos de informe. Para ello, vea los elementos dependientes que hacen referencia al origen de datos compartido.  
  
 Aunque la lista de elementos dependientes le indica si se hace referencia al origen de datos compartido, no indica si el elemento se utiliza de forma activa. Para determinar si el origen de datos compartido o el modelo se usa de manera activa, puede consultar los archivos de registro del equipo del servidor de informes. Si no tiene acceso a los archivos de registro o si éstos no contienen la información deseada, considere la posibilidad de mover el informe a una capeta inaccesible mientras determina su estado actual.  
  
### <a name="to-create-a-shared-data-source-rsds-file-sharepoint-2010"></a>Para crear un archivo de origen de datos compartido (.rsds) (SharePoint 2010)  
  
1.  Haga clic en la pestaña **Documentos** de la cinta de bibliotecas.  
  
2.  En el menú **Nuevo documento** , haga clic en **Origen de datos de informe**.  
  
    > [!NOTE]  
    >  Si no ve el elemento **Origen de datos de informe** en el menú, significa que no se ha habilitado el tipo de contenido del origen de datos de informe. Para obtener más información, consulte [Agregar informe Server tipos de contenido en una biblioteca &#40;Reporting Services en modo integrado de SharePoint&#41;](../../2014/reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  En **Nombre**, escriba un nombre descriptivo para el archivo .rsds.  
  
4.  En **Tipo de origen de datos**, seleccione en la lista el tipo de origen de datos. Para más información, vea [Orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
5.  En **Cadena de conexión**, especifique un puntero al origen de datos y cualquier otra opción de configuración necesaria para establecer una conexión al origen de datos externo. El tipo de origen de datos que esté utilizando determinará la sintaxis de la cadena de conexión. Para obtener más información y ejemplos, vea [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
6.  En **Credenciales**, especifique el modo en que el servidor de informes debe obtener las credenciales para obtener acceso al origen de datos externo. Las credenciales pueden almacenarse, solicitarse, integrarse o configurarse para el procesamiento de informes en modo desatendido.  
  
    -   Seleccione **Autenticación de Windows (integrada)** si quiere acceder a los datos con las credenciales del usuario que ha abierto el informe. No seleccione esta opción si el sitio o la granja de servidores de SharePoint usa la autenticación de formularios o se conecta al servidor de informes a través de una cuenta de confianza. No seleccione esta opción si desea programar el procesamiento de suscripciones o datos para este informe. Esta opción funciona de manera óptima cuando la autenticación Kerberos está habilitada para el dominio o cuando el origen de datos se encuentra en el mismo equipo que el servidor de informes. Si la autenticación Kerberos no está habilitada, las credenciales de Windows solo se pueden pasar a otro equipo. Esto significa que si el origen de datos externo es otro equipo, que requiere una conexión adicional, obtendrá un error en lugar de los datos esperados.  
  
    -   Seleccione **Pedir credenciales** si desea que el usuario especifique sus credenciales cada vez que ejecute el informe. No seleccione esta opción si desea programar el procesamiento de suscripciones o datos para este informe.  
  
    -   Seleccione **Credenciales almacenadas** si desea obtener acceso a los datos mediante un único conjunto de credenciales. Las credenciales se cifran antes de guardarse. Puede seleccionar opciones que determinan el modo en que se autentican las credenciales almacenadas. Seleccione Usar como credenciales de Windows si las credenciales almacenadas pertenecen a una cuenta de usuario de Windows. Seleccione **Establecer contexto de ejecución en esta cuenta** si desea establecer el contexto de ejecución en el servidor de base de datos. En el caso de las bases de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , esta opción establece la función SETUSER. Para más información, vea [SETUSER &#40;Transact-SQL&#41;](/sql/t-sql/statements/setuser-transact-sql).  
  
    -   Seleccione **No se necesitan credenciales** si quiere especificar credenciales en la cadena de conexión o si quiere ejecutar el informe con una cuenta con privilegios mínimos configurada en el servidor de informes. Si esta cuenta no está configurada en el servidor de informes, se solicitarán las credenciales a los usuarios y no se ejecutará ninguna de las operaciones programadas que defina para el informe.  
  
7.  Seleccione **Habilitar este origen de datos** si desea que el origen de datos esté activo. Si el origen de datos está configurado pero no activo, los usuarios recibirán un mensaje de error si intentan utilizar un informe basado en él.  
  
8.  Haga clic en el botón **Probar conexión** para validar la configuración del origen de datos.  
  
    > [!NOTE]  
    >  El botón Probar conexión no se admite para el tipo de origen de datos XML.  
  
9. Haga clic en **Aceptar** para crear el origen de datos compartido.  
  
### <a name="to-view-dependent-items"></a>Para ver elementos dependientes  
  
1.  Abra la biblioteca que contiene el archivo .rsds.  
  
2.  Seleccione el origen de datos compartido.  
  
3.  Haga clic para que se muestre una flecha hacia abajo y seleccione **Ver elementos dependientes**.  
  
     En el caso de los modelos de informe, la lista de elementos dependientes muestra los informes creados en el Generador de informes. En el caso de los orígenes de datos compartidos, la lista de elementos dependientes puede incluir tanto informes como modelos de informe.  
  
### <a name="to-delete-a-shared-data-source-rsds-file"></a>Para eliminar un archivo de origen de datos compartido (.rsds)  
  
1.  Abra la biblioteca que contiene el archivo .rsds.  
  
2.  Seleccione el origen de datos compartido.  
  
3.  Haga clic para que se muestre una flecha hacia abajo y haga clic en **Eliminar**.  
  
 Si elimina por error un origen de datos compartido que tenía intención de conservar, puede crear uno nuevo que contenga la misma información de conexión. Después de volver a crear el origen de datos compartido, debe abrir cada uno de los informes y modelos que usaba el origen de datos y seleccionar el origen de datos compartido. El nuevo elemento de origen de datos compartido puede tener un nombre, unas credenciales o una sintaxis de la cadena de conexión distintos de los del eliminado. Mientras la conexión se resuelva en el mismo origen de datos, las propiedades del origen de datos pueden variar con respecto a los valores originales.  
  
 Tenga cuidado al eliminar un modelo de informe. Si elimina un modelo, no podrá abrir ni modificar ningún informe basado en ese modelo en el Generador de informes. Si elimina accidentalmente un modelo utilizado por los informes existentes, deberá volver a generar el modelo, deberá volver a crear y guardar todos los informes que utilicen dicho modelo y deberá volver a especificar la seguridad de elementos de modelo que desee utilizar. No basta con volver a generar el modelo y luego adjuntarlo a un informe existente.  
  
## <a name="see-also"></a>Vea también  
 [Especificación de información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
