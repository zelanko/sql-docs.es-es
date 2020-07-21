---
title: Crear un origen de datos de informe | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: bd6662c7-ffbe-479d-8944-3dc858340998
author: minewiskan
ms.author: owend
ms.openlocfilehash: f9d009b6cae346fd2b16d0651b0e905a0fb9e7eb
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536267"
---
# <a name="create-a-report-data-source"></a>Crear un origen de datos de informe
  Para que Power View se conecte con un modelo multidimensional, es necesario crear una definición de origen de datos de informe compartido, también conocida como un archivo .rsds, en una biblioteca de SharePoint. El archivo .rsds especifica el nombre de una instancia de servidor de Analysis Services, el tipo de conexión, la cadena de conexión y las credenciales utilizadas para conectarse con el modelo multidimensional. Cuando un usuario hace clic en el archivo .rsds, se abre un nuevo informe de Power View vacío (un archivo .rdlx) en el explorador.  
  
 Para crear una conexión .rsds, es necesario tener instalado SQL Server 2012 (o posterior) Reporting Services y el complemento Reporting Services para SharePoint 2010 o SharePoint 2013.  
  
## <a name="create-a-report-data-source-rsds-connection-to-a-multidimensional-model"></a>Crear una conexión de origen de datos de informe (.rsds) con un modelo multidimensional  
 Antes de empezar, debe conocer:  
  
-   El nombre de la instancia de servidor de Analysis Services que se está ejecutando en modo multidimensional.  
  
-   El nombre de la base de datos multidimensional con la que desea conectarse.  
  
-   El nombre del cubo, si hay más de uno.  
  
-   (Opcional) Nombre de la perspectiva.  
  
-   (Opcional) Identificador de configuración regional.  
  
#### <a name="to-create-a-shared-report-data-source-rsds-file-sharepoint-2010"></a>Para crear un archivo de origen de datos compartido (.rsds) (SharePoint 2010)  
  
1.  Haga clic en la pestaña **Documentos** de la cinta de bibliotecas.  
  
2.  Haga clic en **nuevo documento**  >  **origen de datos de informe**.  
  
    > [!NOTE]  
    >  Si no ve el elemento **Origen de datos de informe** en el menú, significa que no se ha habilitado el tipo de contenido del origen de datos de informe para esta biblioteca. Para obtener más información, vea [agregar tipos de contenido del servidor de informes a una biblioteca &#40;Reporting Services en el modo integrado de SharePoint&#41;](../../reporting-services/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  En la página **Propiedades del origen de datos** , en **Nombre**, escriba un nombre para el archivo de conexión .rsds.  
  
4.  En **Tipo de origen de datos**, seleccione **Microsoft BI Semantic Model para Power View**.  
  
5.  En **Cadena de conexión**, especifique el nombre del servidor de Analysis Services, el nombre de la base de datos, el nombre del cubo y los valores opcionales.  
  
     Cadena de conexión: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'`  
  
    > [!NOTE]  
    >  Si hay más de un cubo, es necesario especificar un nombre de cubo.  
  
     (Opcional) Los cubos pueden tener perspectivas que proporcionan a los usuarios unas vistas especiales en las que únicamente están visibles ciertas dimensiones y/o grupos de medidas en el cliente. Para especificar una perspectiva, escriba el nombre de esta como un valor de la propiedad Cube: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<perspectivename>'`  
  
     (Opcional) Los cubos pueden tener traducciones de datos y metadatos especificados para varios idiomas dentro del modelo. Para ver las traducciones (datos y metadatos), necesita agregar la propiedad "identificador regional" a la cadena de conexión:`Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>'; Locale Identifier=<identifier number>`  
  
6.  En **Credenciales**, especifique el modo en que el servidor de informes debe obtener las credenciales para obtener acceso al origen de datos externo.  
  
    -   Seleccione **Autenticación de Windows (integrada)** si quiere acceder a los datos con las credenciales del usuario que ha abierto el informe. No seleccione esta opción si el sitio o la granja de servidores de SharePoint usa la autenticación de formularios o se conecta al servidor de informes a través de una cuenta de confianza. No seleccione esta opción si desea programar el procesamiento de suscripciones o datos para este informe. Esta opción funciona de manera óptima cuando la autenticación Kerberos está habilitada para el dominio o cuando el origen de datos se encuentra en el mismo equipo que el servidor de informes. Si la autenticación Kerberos no está habilitada, las credenciales de Windows solo se pueden pasar a otro equipo. Esto significa que si el origen de datos externo es otro equipo, que requiere una conexión adicional, obtendrá un error en lugar de los datos esperados.  
  
    -   Seleccione **Pedir credenciales** si desea que el usuario especifique sus credenciales cada vez que ejecute el informe. No seleccione esta opción si desea programar el procesamiento de suscripciones o datos para este informe.  
  
    -   Seleccione **Credenciales almacenadas** si desea obtener acceso a los datos mediante un único conjunto de credenciales. Las credenciales se cifran antes de guardarse. Puede seleccionar opciones que determinan el modo en que se autentican las credenciales almacenadas. Seleccione Usar como credenciales de Windows si las credenciales almacenadas pertenecen a una cuenta de usuario de Windows. Seleccione **Establecer contexto de ejecución en esta cuenta** si desea establecer el contexto de ejecución en el servidor de base de datos.  
  
    -   Seleccione **No se necesitan credenciales** si especifica las credenciales en la cadena de conexión o si quiere ejecutar el informe con una cuenta con privilegios mínimos.  
  
7.  Haga clic en **Probar conexión** para validar la conexión.  
  
8.  Seleccione **Habilitar este origen de datos** si desea que el origen de datos esté activo. Si el origen de datos está configurado pero no activo, los usuarios recibirán un mensaje de error si intentan crear un informe.  
  
  
