---
title: Crear una conexión de modelo semántico de BI en una base de datos de modelo Tabular | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9141a382cf30157849de3cb0d54bff882790b48d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-bi-semantic-model-connection-to-a-tabular-model-database"></a>Crear una conexión de modelo semántico de BI a una base de datos de modelo tabular
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Utilice la información de este tema para configurar una conexión de modelo semántico de BI que se redirija a una base de datos modelo tabular que se ejecuta en una instancia de Analysis Services fuera de la granja de SharePoint.  
  
 Después de crear una conexión de modelo semántico de BI y configurar los permisos de SharePoint y Analysis Services, los usuarios pueden utilizarla como origen de datos para Excel o informes de [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] .  
  
 En este tema se incluyen las secciones siguientes. Realice cada tarea en el orden indicado.  
  
 [Requisitos previos de revisión](#bkmk_prereq)  
  
 [Conceder permisos administrativos de Analysis Services a aplicaciones de servicios compartidos](#bkmk_ssas)  
  
 [Conceder permisos de lectura en la base de datos de modelo tabular](#bkmk_BISM)  
  
 [Crear una conexión de modelo semántico de BI a una base de datos de modelo tabular](#bkmk_connect)  
  
 [Configurar permisos de SharePoint en la conexión de modelo semántico de BI](#bkmk_permissions)  
  
 [Pasos siguientes](#bkmk_next)  
  
##  <a name="bkmk_prereq"></a> Requisitos previos de revisión  
 Debe tener permisos de contribución o superiores para poder crear un archivo de conexión de modelo semántico de BI.  
  
 Debe tener una biblioteca que admita el tipo de contenido de la conexión de modelo semántico de BI. Para más información, vea [Agregar un tipo de contenido de conexión de modelo semántico de BI a una biblioteca &#40;PowerPivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/add-bi-semantic-model-connection-content-type-to-library.md).  
  
 Debe conocer el servidor y el nombre de la base de datos para los que va a configurar una conexión de modelo semántico de BI. Analysis Services debe estar configurado para el modo tabular. Las bases de datos que se ejecutan en el servidor deben ser bases de datos de modelos tabulares. Para obtener instrucciones sobre cómo comprobar el modo del servidor, vea [Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 En determinados casos, los servicios compartidos en un entorno de SharePoint deben tener permisos administrativos en la instancia de Analysis Services. Entre estos servicios se hallan las aplicaciones de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , las aplicaciones de servicio de Reporting Services y las aplicaciones de servicio de PerformancePoint. Para poder conceder permisos administrativos, debe conocer la identidad de estas aplicaciones de servicio. Puede usar Administración central para determinar la identidad.  
  
 Debe ser administrador del servicio de SharePoint para ver la información de seguridad en Administración central.  
  
 Debe ser administrador del sistema de Analysis Services para conceder derechos administrativos en Management Studio.  
  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint a través de las aplicaciones web que utilizan el modo de autenticación clásico. Las conexiones de modelo semántico de BI a orígenes de datos externos dependen del inicio de sesión en modo clásico Para más información, vea [Power Pivot Authentication and Authorization](../../analysis-services/power-pivot-sharepoint/power-pivot-authentication-and-authorization.md).  
  
 Todos los equipos y usuarios que forman parte de la secuencia de conexión deben estar en el mismo dominio o en dominios de confianza (confianza bidireccional).  
  
##  <a name="bkmk_ssas"></a> Conceder permisos administrativos de Analysis Services a aplicaciones de servicios compartidos  
 Las conexiones que tienen como origen SharePoint y como destino una base de datos modelo tabular de un servidor de Analysis Services en ocasiones se establecen a través de un servicio compartido que actúa en nombre del usuario que solicita los datos. El servicio que realiza la solicitud podría ser una aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , una aplicación de servicio de Reporting Services o una aplicación de servicio de PerformancePoint. Para que la conexión se realice correctamente, el servicio debe tener permisos administrativos en el servidor de Analysis Services. En Analysis Services, solo se permite a un administrador realizar una conexión suplantada en nombre de otro usuario.  
  
 Los permisos administrativos son necesarios cuando la conexión se usa en las siguientes condiciones:  
  
-   Cuando se comprueba la información de conexión durante la configuración de un archivo de conexión de modelo semántico de BI.  
  
-   Al iniciar un informe de la vista avanzada mediante una conexión de modelo semántico de BI.  
  
-   Al rellenar un elemento web de PerformancePoint con una conexión de modelo semántico de BI.  
  
 Para asegurarse de que estos comportamientos se realizan según lo esperado, conceda permisos administrativos a cada identidad de servicio en la instancia de Analysis Services. Utilice las instrucciones siguientes para conceder los permisos necesarios.  
  
 **Agregar las identidades de servicio al rol de administrador del servidor**  
  
1.  En SQL Server Management Studio, conéctese a la instancia de Analysis Services.  
  
2.  Haga clic con el botón derecho en el nombre del servidor y seleccione **Propiedades**.  
  
3.  Haga clic en **Seguridad**y luego en **Agregar**. Escriba la cuenta de usuario de Windows que se utiliza para ejecutar la aplicación de servicio.  
  
     Puede usar Administración central para determinar la identidad. En la sección Seguridad, abra **Configurar cuentas de servicio** para ver qué cuenta de Windows está asociada con el grupo de aplicaciones de servicio usado en cada aplicación. A continuación, siga las instrucciones que se detallan en este tema para conceder los permisos administrativos de la cuenta.  
  
##  <a name="bkmk_BISM"></a> Conceder permisos de lectura en la base de datos de modelo tabular  
 Dado que la base de datos se ejecuta en un servidor que es externo a la granja, parte de la configuración de las conexiones incluirá conceder permisos de base de datos en el servidor back-end de Analysis Services. Analysis Services utiliza un modelo de permisos basado en roles. Los usuarios que se conectan a bases de datos modelo deben hacerlo con permisos de lectura o superiores, a través de un rol que conceda acceso de lectura a sus miembros.  
  
 Los roles y, a veces, la pertenencia a roles, se definen cuando el modelo se crea en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. No puede utilizar SQL Server Management Studio para crear roles, pero puede usarlo para agregar miembros a un rol que ya está definido. Para obtener más información sobre cómo crear roles, consulte [crear y administrar funciones](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
#### <a name="assign-role-membership"></a>Asignar pertenencia a roles  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda la base de datos en el Explorador de objetos y, a continuación, **Roles**. Debe ver un rol que ya está definido. Si no existe un rol, póngase en contacto con el autor del modelo y solicite que se agregue uno o un rol. Es necesario volver a implementar el modelo para que el rol esté visible en Management Studio.  
  
2.  Haga clic con el botón derecho en el rol y seleccione **Propiedades**.  
  
3.  En la página Pertenencia, agregue el grupo de Windows y las cuentas de usuario que requieren acceso.  
  
##  <a name="bkmk_connect"></a> Crear una conexión de modelo semántico de BI a una base de datos de modelo tabular  
 Después de establecer los permisos en Analysis Services, puede volver a SharePoint y crear una conexión de modelo semántico de BI.  
  
1.  En la biblioteca que contendrá la conexión de modelo semántico de BI, haga clic en **Documentos** en la cinta de opciones de SharePoint.  
  
2.  Haga clic en la flecha abajo en Nuevo documento y seleccione **Archivo de conexión de modelo semántico de BI** para abrir la página Nueva conexión de modelo semántico de BI.  
  
3.  Establezca las propiedades **Servidor** y **Base de datos** . Si no está seguro del nombre de la base de datos, utilice SQL Server Management Studio para ver una lista de las bases de datos implementadas en el servidor.  
  
     **Nombre del servidor** es el nombre de red del servidor, la dirección IP o el nombre de dominio completo (por ejemplo, myserver.mydomain.corp.adventure-works.com). Si el servidor está instalado como una instancia con nombre, escriba el nombre de servidor en este formato: nombredeequipo\nombredeinstancia.  
  
     **Base de datos** debe ser una base de datos tabular que esté disponible en el servidor. No especifique otro archivo de conexión de modelo semántico de BI, un archivo de conexión de datos de Office (.odc), una base de datos OLAP de Analysis Services o un libro de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obtener el nombre de la base de datos, puede usar Management Studio para conectarse al servidor y ver la lista de bases de datos disponibles. Use la página de propiedades de la base de datos para asegurarse de que tiene el nombre correcto.  
  
4.  Haga clic en **Aceptar** para guardar la página. En este momento, la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] comprobará la conexión.  
  
     La comprobación se realiza correctamente si la información de conexión es correcta y ha concedido permisos administrativos a la aplicación de servicio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para que pueda conectarse a Analysis Services como el usuario actual.  
  
     La comprobación no se realiza correctamente si la información de conexión es incorrecta o la aplicación de servicio no tiene permisos. Aparecerá un mensaje de validación en la página donde se le preguntará si desea guardar el archivo. Si sabe que la conexión es válida, debe guardar el archivo de todos modos, porque el error es el resultado de la falta de permisos y no de que la información de conexión no sea válida.  
  
     Puede comprobar la conexión utilizándola en Excel o en la vista avanzada para conectarse con la base de datos modelo tabular. Si la conexión del origen de datos se realiza correctamente, la conexión es válida a pesar de la advertencia de comprobación.  
  
##  <a name="bkmk_permissions"></a> Configurar permisos de SharePoint en la conexión de modelo semántico de BI  
 La capacidad de utilizar una conexión de modelo semántico de BI como origen de datos en un libro de Excel o un informe de Reporting Services requiere permisos de **Lectura** en el elemento de conexión de modelo semántico de BI de una biblioteca de SharePoint. El nivel de permiso de lectura incluye el permiso **Abrir elementos** , que permite descargar la información de la conexión de modelo semántico de BI en una aplicación de escritorio de Excel.  
  
 Hay varias maneras de conceder permisos de SharePoint. Las instrucciones siguientes explican cómo crear un grupo denominado **Usuarios de BISM** que tenga el nivel de permiso de **Lectura** .  
  
 Debe ser propietario del sitio para cambiar los permisos.  
  
1.  En Acciones del sitio, haga clic en **Permisos de sitio**.  
  
2.  Haga clic **Crear grupo** y asigne al nuevo grupo el nombre **Usuarios de BISM**.  
  
3.  Elija el nivel de permiso de **Lectura** y haga clic en **Crear**.  
  
4.  Seleccione **Usuarios de BISM** en usuarios y grupos.  
  
5.  Seleccione Nuevo, haga clic en **Agregar usuarios**y, a continuación, agregue cuentas de usuario o grupo.  
  
     Estos usuarios y grupos tendrán ahora permisos de Lectura en el sitio, incluidas todas las bibliotecas y las listas que hereden permisos del nivel de sitio. Si estos permisos son demasiado elevados, puede quitar selectivamente este grupo de determinadas bibliotecas, listas, o elementos.  
  
 Para quitar selectivamente permisos en el nivel de elemento, haga lo siguiente:  
  
1.  En una biblioteca, seleccione un documento. Haga clic en la flecha abajo a la derecha y después haga clic en **Administrar permisos**.  
  
2.  Un elemento hereda, de forma predeterminada, los permisos. Para cambiar los permisos de documentos individuales en esta biblioteca, haga clic en **Dejar de heredar permisos**.  
  
3.  Active la casilla junto a **Usuarios de BISM**.  
  
4.  Haga clic en **Quitar permisos de usuario**.  
  
##  <a name="bkmk_next"></a> Pasos siguientes  
 Después de crear y proteger una conexión de modelo semántico de BI, podrá especificarla como origen de datos. Para obtener más información, vea [Usar una conexión de modelo semántico de BI en Excel o Reporting Services](../../analysis-services/power-pivot-sharepoint/use-a-bi-semantic-model-connection-in-excel-or-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Conexión del modelo semántico de BI de PowerPivot &#40;.bism&#41;](../../analysis-services/power-pivot-sharepoint/power-pivot-bi-semantic-model-connection-bism.md)   
 [Creación de una conexión de modelo semántico de BI a un libro PowerPivot](../../analysis-services/power-pivot-sharepoint/create-a-bi-semantic-model-connection-to-a-power-pivot-workbook.md)  
  
  
