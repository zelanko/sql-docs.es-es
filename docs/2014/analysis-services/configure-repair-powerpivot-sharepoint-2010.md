---
title: Configurar o reparar PowerPivot para SharePoint 2010 (herramienta de configuración de PowerPivot) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d61f49c5-efaa-4455-98f2-8c293fa50046
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1d89de37de81311b1f4a884eeaf434e8247da633
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174474"
---
# <a name="configure-or-repair-powerpivot-for-sharepoint-2010-powerpivot-configuration-tool"></a>Configurar o reparar PowerPivot para SharePoint 2010 (Herramienta de configuración de PowerPivot)
  Para configurar o reparar una instalación de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] PowerPivot para SharePoint 2010, use la Herramienta de configuración de PowerPivot. La herramienta de configuración comienza examinando el sistema y devuelve una lista de las acciones necesarias para completar o reparar una instalación. El Asistente para la instalación de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] instala la herramienta de configuración de PowerPivot para SharePoint 2010 y una herramienta de configuración de PowerPivot para SharePoint 2013. En este tema se describe la herramienta de configuración de PowerPivot para SharePoint 2010. Para obtener más información sobre SharePoint 2010, vea [configurar o reparar PowerPivot para SharePoint 2013 &#40;herramienta de configuración de PowerPivot&#41;](power-pivot-sharepoint/configure-or-repair-power-pivot-for-sharepoint-2013.md).

 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010

 

##  <a name="before-you-start"></a><a name="bkmk_before"></a>Antes de empezar
 La herramienta de configuración de PowerPivot para SharePoint 2010 examina los archivos de programa, los valores del Registro y los puertos disponibles. Para sacar el máximo partido de estas herramientas, vea lo siguiente.

-   Requisitos generales para ejecutar la herramienta de configuración, [PowerPivot Configuration Tools](power-pivot-sharepoint/power-pivot-configuration-tools.md).

-   PowerPivot para SharePoint 2010 necesita que las aplicaciones web estén configuradas para la autenticación en modo clásico. Si es la herramienta de configuración de PowerPivot para SharePoint 2010 quien crea la aplicación, la aplicación se configura para el modo clásico.

-   El puerto 80 debe estar disponible; una de las tareas seleccionadas necesita la herramienta de configuración para crear y configurar una aplicación web.

##  <a name="using-the-powerpivot-configuration-tool"></a><a name="bkmk_using"></a>Usar la herramienta de configuración de PowerPivot
 La primera página de la herramienta proporciona un resumen de los valores de entrada que se usarán para configurar la granja de SharePoint. Además de los valores de entrada que proporcione, se usarán los valores predeterminados para configurar el sistema. Los nombres predeterminados se utilizan con las aplicaciones de servicio, las bases de datos de aplicación de servicio y las propiedades de la aplicación de servicio.

> [!TIP]
>  Si la herramienta de configuración de PowerPivot examina el equipo y devuelve una lista de tareas en blanco en el panel izquierdo, no hay ninguna característica o valor que necesite configuración. Para modificar la configuración de SharePoint o PowerPivot, use Windows PowerShell o las páginas de administración de Administración central de SharePoint. Para obtener más información, vea [Administración y configuración del servidor PowerPivot en administración central](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md).

 Los valores de las cuentas de servicio se usan para varios servicios. Por ejemplo, la herramienta de configuración de PowerPivot usa la cuenta predeterminada de la primera página para establecer todas las identidades del grupo de aplicaciones. Puede cambiar estas cuentas posteriormente modificando las propiedades de la aplicación de servicio en Administración central.

-   La excepción a esta regla en la herramienta de configuración de PowerPivot para SharePoint 2010 es la cuenta de servicio de Analysis Services. Esta cuenta se especifica durante la instalación y se escribe una contraseña para esta cuenta en la acción **registrar SQL Server Analysis Services (PowerPivot en el servidor local)** . La página de resumen no incluye un campo para esta contraseña, por lo que debe asegurarse de introducirla en la página para esa acción.

 La herramienta proporciona una interfaz con pestañas que incluye entradas de parámetros, el script de Windows PowerShell y mensajes de estado.

 La herramienta de configuración de PowerPivot usa Windows PowerShell para configurar el servidor. Puede hacer clic en la pestaña **script** para revisar el script de Windows PowerShell.

 ![Interfaz de usuario de la herramienta de configuración](media/ssas-pctui.gif "Interfaz de usuario de la herramienta de configuración")

##  <a name="configuration-steps"></a><a name="bkmk_steps"></a>Pasos de configuración
 El vínculo a la herramienta de configuración solo está visible cuando PowerPivot para SharePoint 2010 está instalado en el servidor local.

1.  En el menú **Inicio** , elija **Todos los programas**, haga clic en [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], en **Herramientas de configuración**y, a continuación, en **Herramienta de configuración de PowerPivot**.

2.  Haga clic en **Configurar o reparar PowerPivot para SharePoint**.

3.  Expanda la ventana al tamaño máximo. Aparecerá una barra de botones en la parte inferior de la ventana con los comandos **Validar****Ejecutar**y **Salir** .

4.  **Cuenta predeterminada** : en la pestaña Parámetros, escriba una cuenta de usuario de dominio para **Nombre de usuario de cuenta predeterminada**. Esta cuenta se usa para aprovisionar servicios esenciales, incluido el grupo de aplicaciones del servicio PowerPivot. No especifique ninguna cuenta integrada, como Network Service o Local System. La herramienta bloquea las configuraciones que especifican cuentas integradas.

     **Frase de contraseña** : escriba una frase de contraseña. En el caso de una nueva granja de SharePoint, la frase de contraseña se usa siempre que se agrega un nuevo servidor o una nueva aplicación a la granja de servidores de SharePoint. Si se trata de una granja existente, escriba la frase de contraseña que le permita agregar una aplicación de servidor a la granja.

5.  **Puerto** : opcionalmente, escriba un número de puerto para conectarse a la aplicación web de Administración central o use el número generado aleatoriamente proporcionado. La herramienta de configuración comprueba que el número está disponible antes de ofrecerlo como opción.

6.  Haga clic en **registrar SQL Server Analysis Services (PowerPivot) en el servidor local**.

     Escriba la contraseña de la cuenta de servicio de Analysis Services.

7.  Opcionalmente, revise los valores restantes de entrada utilizados para completar cada acción. Para obtener más información acerca de cada uno de ellos, consulte [Valores de entrada utilizados para configurar el servidor](#bkmk_input) en este tema.

8.  Si lo desea, quite cualquier acción que no desee procesar. Por ejemplo, si desea configurar el Servicio de almacenamiento seguro más adelante, haga clic en **Configurar el servicio de almacenamiento seguro**y, a continuación, desactive la casilla **Incluir esta acción en la lista de tareas**.

9. Haga clic en **Validar** para comprobar si la herramienta tiene suficiente información para procesar las acciones de la lista.

    > [!NOTE]
    >  Si obtiene un error de configuración de la granja, podría ser porque no está instalado SharePoint 2010 Server SP1.

10. Haga clic en **Ejecutar** para procesar todas las acciones de la lista de tareas. El botón **Ejecutar** se habilita después de validar las acciones. Si **Ejecutar** no está habilitado, haga clic en **Validar** primero.

11. [Comprobar una instalación de PowerPivot para SharePoint](instances/install-windows/verify-a-power-pivot-for-sharepoint-installation.md).

##  <a name="input-values-used-to-configure-the-server"></a><a name="bkmk_input"></a>Valores de entrada utilizados para configurar el servidor
 La herramienta de configuración de PowerPivot utilizará una combinación de los valores de entrada que escriba el usuario con los valores predeterminados que la herramienta detecte o utilice automáticamente.

 La lista de acciones mostrada en la herramienta de configuración depende de la configuración actual de la granja de SharePoint. Por ejemplo, si la granja de servidores de SharePoint ya está configurada, no se mostrará ninguna acción en la herramienta. Puede ejecutar la herramienta en cualquier momento para configurar, reparar o detectar errores de configuración. Si en la granja no se ejecutan servicios requeridos, como Excel Services o el Servicio de almacenamiento seguro, la herramienta detectará los servicios que faltan y proporcionará opciones para habilitarlos. Si no se requiere ninguna acción, la lista de tareas estará vacía.

 En la tabla siguiente se describen los valores usados para configurar el servidor.

|Página|Valor de entrada|Source|Descripción|
|----------|-----------------|------------|-----------------|
|**Configurar o reparar PowerPivot para SharePoint**|Cuenta predeterminada|Usuario actual|La cuenta predeterminada es una cuenta de usuario de Windows de dominio que se utiliza para proporcionar servicios compartidos en la granja. Se utiliza para proporcionar la aplicación de servicio PowerPivot, el Servicio de almacenamiento seguro, Excel Services, la identidad del grupo de aplicaciones web, el administrador de la colección de sitios, y la cuenta de actualización de datos desatendida de PowerPivot.<br /><br /> De forma predeterminada, la herramienta especifica la cuenta de dominio del usuario actual. A menos que esté configurando un servidor con fines de evaluación, debe reemplazar este con otra cuenta de usuario de dominio.<br /><br /> También puede cambiar las identidades de servicio posteriormente, mediante Administración central.<br /><br /> Opcionalmente, en la herramienta de configuración de PowerPivot, puede especificar cuentas dedicadas para:<br /><br /> Aplicación Web, mediante la página **crear aplicación web predeterminada** (suponiendo que la herramienta está creando una aplicación web para la granja de servidores).<br /><br /> Cuenta de actualización de datos desatendida de PowerPivot, mediante la página **crear cuenta desatendida para la actualización de datos** de esta herramienta.|
||Servidor de bases de datos|Instancia con nombre local de PowerPivot, si está disponible|Si una instancia del motor de base de datos se instala como una instancia con nombre de PowerPivot, la herramienta rellenará el campo del servidor de bases de datos con esta instancia. Si no ha instalado el motor de base de datos, este campo está vacío. Debe proporcionar una instancia. Puede ser cualquier versión o edición de SQL Server que se admita en granjas de servidores de SharePoint.|
||Passphrase|Datos proporcionados por el usuario|Si va a crear una nueva granja, la frase de contraseña que escriba será la frase de contraseña para la granja. Si va a agregar PowerPivot para SharePoint a una granja existente, debe proporcionar la frase de contraseña que se definió para la granja cuando se creó.|
||Puerto de Administración central de SharePoint|Valor predeterminado, si es necesario|Si la granja no está configurada, la herramienta proporcionará opciones para crearla, incluido un extremo HTTP en Administración central. Usa de forma predeterminada un número de puerto generado aleatoriamente que no esté en uso.|
|**Configurar una nueva granja**|Servidor de bases de datos<br /><br /> Cuenta de granja<br /><br /> Frase de contraseña<br /><br /> Puerto de Administración central de SharePoint|Valor predeterminado, si es necesario|Las configuraciones usan como valor predeterminado lo que especificó en la página principal.|
|**Configurar instancias de servicio local**|Contraseña de la cuenta de servicio de Analysis Services.|Datos proporcionados por el usuario|Debe escribir la contraseña de la cuenta de servicio de Analysis Services en la página **registrar SQL Server Analysis Services (PowerPivot) en el servidor local** .<br /><br /> La cuenta de servicio se especificó durante la instalación. Ahora debe escribir la contraseña como entrada para registrar la instancia del servicio local con SharePoint.|
|**Crear una aplicación de servicio PowerPivot**|Nombre de aplicación de servicio PowerPivot|Default|El nombre predeterminado es Aplicación de servicio PowerPivot predeterminada. Podrá sustituirlo por otro valor de la herramienta.|
||Servidor de la base de datos de aplicación de servicio PowerPivot|Default|El servidor de bases de datos que va a hospedar la base de datos de aplicación de servicio PowerPivot. El nombre del servidor predeterminado es el mismo servidor de bases de datos usado para la granja. Podrá sustituirlo por otro valor de la herramienta.|
||Nombre de la base de datos de la aplicación de servicio PowerPivot|Default|El nombre predeterminado de la base de datos se basa en el nombre de aplicación de servicio, seguido de un GUID para garantizar un nombre único. Podrá sustituirlo por otro valor de la herramienta.|
||Actualizar libros antes de habilitar la actualización de datos|Datos proporcionados por el usuario|La actualización de datos genera un error y no se admite para los libros de SQL Server 2008 R2 PowerPivot. La opción **Actualizar libros para habilitar la actualización de datos** actualiza los libros a SQL Server versión 2012 de PowerPivot.|
|**Crear aplicación web predeterminada**|Nombre de aplicación web|Valor predeterminado, si es necesario|Si no existe ninguna aplicación web, la herramienta creará una. La aplicación web se configurará para la autenticación en modo clásico y para escuchar en el **puerto 80**. El tamaño máximo de carga de archivos se establece en 2047 MB, el máximo permitido por SharePoint. Se usa el tamaño máximo de carga de archivos para permitir archivos grandes de PowerPivot.|
||URL|Valor predeterminado, si es necesario|La herramienta crea una dirección URL basada en el nombre del servidor, con las mismas convenciones de nomenclatura de archivos que SharePoint.|
||Grupo de aplicaciones web|Valor predeterminado, si es necesario|La herramienta crea un grupo de aplicaciones predeterminado en IIS.|
||Cuenta y contraseña del grupo de aplicaciones web|Valor predeterminado, si es necesario|La cuenta del grupo de aplicaciones se basa en la cuenta predeterminada, pero puede sustituirla en la herramienta.|
||Servidor de la base de datos de aplicación web|Valor predeterminado, si es necesario|Se preselecciona la instancia predeterminada de la base de datos para almacenar la base de datos de aplicación, pero puede especificar otra instancia de SQL Server en la herramienta.|
||Nombre de la base de datos de aplicación web|Valor predeterminado, si es necesario|El nombre de la base de datos se basa en las convenciones de nomenclatura de archivos de SharePoint, pero puede elegir un nombre diferente.|
|**Implementar solución de aplicación web**|URL|Valor predeterminado, si es necesario|La dirección URL predeterminada es la de la aplicación web predeterminada.|
||Tamaño de archivo máximo (en MB)|Valor predeterminado, si es necesario|El valor predeterminado es 2047. Las bibliotecas de documentos de SharePoint también tienen un tamaño máximo y el valor de PowerPivot no debe superar el valor de la biblioteca de documentos. Para obtener más información, vea [configurar el tamaño máximo de carga de archivos &#40;PowerPivot para SharePoint&#41;](power-pivot-sharepoint/configure-maximum-file-upload-size-power-pivot-for-sharepoint.md).|
|**Crear una colección de sitios**|Administrador del sitio|Valor predeterminado, si es necesario|La herramienta utiliza la cuenta predeterminada. Puede sustituirlo en la página **Crear colección de sitios** .|
||Correo electrónico de contacto|Valor predeterminado, si es necesario|Si Microsoft Outlook está configurado en el servidor, la herramienta usará la dirección de correo electrónico del usuario actual. Si no, se utiliza un valor de marcador de posición.|
||Dirección URL del sitio|Valor predeterminado, si es necesario|La herramienta crea la dirección URL del sitio, utilizando las mismas convenciones de nomenclatura de direcciones URL que SharePoint.|
||Título del sitio|Valor predeterminado, si es necesario|La herramienta agrega **Sitio de PowerPivot** como título predeterminado.|
|**Activar la característica de PowerPivot en una colección de sitios**|Dirección URL del sitio||Dirección URL de la colección de sitios para la que va a activar las características de PowerPivot.|
||Habilitar la característica premium para este sitio||Habilite la característica "PremiumSite" del sitio de SharePoint.|
|**Crear una aplicación de servicio de almacenamiento seguro**|Nombre de la aplicación de servicio||Escriba el nombre de la aplicación de servicio de almacenamiento seguro.|
||Servidor de bases de datos||Escriba el nombre del servidor de bases de datos que se usará para la aplicación de servicio de almacenamiento seguro.|
|**Crear un proxy de aplicación de servicio de almacenamiento seguro**|Nombre de la aplicación de servicio||Escriba el nombre de la aplicación de servicio de almacenamiento seguro.|
||Proxy de aplicación de servicio||Escriba el nombre del proxy de aplicación de servicio de almacenamiento seguro.  El nombre aparecerá en el grupo de conexiones predeterminado que asocia las aplicaciones con las aplicaciones web de contenido de SharePoint.|
|**Actualizar la clave maestra del servicio de almacenamiento seguro**|Proxy de aplicación de servicio||Escriba el nombre del proxy de aplicación de servicio de almacenamiento seguro|
||Passphrase||La clave maestra se usa para el cifrado de datos. De forma predeterminada, la frase de contraseña que se usa para generar la clave es la misma que se usa para aprovisionar servidores nuevos en la granja. Puede reemplazar la frase de contraseña predeterminada con una frase de contraseña única.|
|**Crear una cuenta desatendida para la actualización de la actualización**|Id. de la aplicación de destino||El identificador de la aplicación puede ser texto descriptivo.|
||Nombre descriptivo de la aplicación de destino|||
||Nombre de usuario y contraseña de la cuenta desatendida||Escriba las credenciales de una cuenta de usuario de Windows usada por la aplicación de destino y que se emplea para ejecutar la actualización de datos desatendida.|
||Dirección URL del sitio||Escriba la dirección URL de la colección de sitios asociada a la aplicación de destino. Para asociarla a colecciones de sitios adicionales, use Administración central de SharePoint.|
|**Crear nueva aplicación de servicio de Excel Services**|Nombre de la aplicación de servicio||Escriba un nombre de aplicación de servicio. Se creará una base de datos de aplicación de servicio con el mismo nombre en el servidor de base de datos de la granja de servidores de SharePoint.|
|**Agregar MSOLAP.5 como proveedor de confianza**|Nombre de la aplicación de servicio||Excel Services en SharePoint 2010 usa el proveedor OLE DB de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para conectarse a datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Este paso agregará la versión del proveedor OLE DB instalado con PowerPivot para SharePoint, como un proveedor de confianza a Excel Services.|
||Nombre del servidor PowerPivot|||
|||||

 Si la herramienta de configuración de PowerPivot crea la granja, crea las bases de datos necesarias en el servidor de bases de datos, usando las mismas convenciones de nomenclatura de archivos que SharePoint. No se puede cambiar el nombre de la base de datos de la granja.

 Si la herramienta crea una colección de sitios, crea una base de datos de contenido en el servidor de bases de datos, utilizando las mismas convenciones de nomenclatura de archivos que SharePoint. No se puede cambiar el nombre de la base de datos de contenido.

##  <a name="next-steps"></a><a name="bkmk_nextsteps"></a> Pasos siguientes
 Después de completar una instalación del servidor, se deben realizar varias tareas posteriores:

-   Conceda permisos de SharePoint a los individuos y a los grupos. Esta tarea es necesaria para permitir el acceso a los sitios y al contenido.

-   Cambie las identidades del grupo de aplicaciones de servicio para que se ejecute en una cuenta diferente. Para que la implementación de SharePoint sea segura, es recomendable especificar identidades diferentes para los servicios y las aplicaciones.

-   Cree sitos de confianza adicionales en Excel Services para que pueda variar los permisos y la configuración que mejor funcionen para el acceso a datos PowerPivot.

-   Instale ADO.NET Data Services 3.5 SP1 para habilitar la exportación de fuentes de distribución de datos desde listas de SharePoint.

-   Instale los proveedores de datos que se usan normalmente para habilitar la actualización de datos del servidor.

-   Descargue la herramienta de creación de PowerPivot en el equipo de estación de trabajo para crear un libro PowerPivot y, a continuación, publíquelo en SharePoint. Al instalar la herramienta y publicar un libro PowerPivot se completa el ciclo de instalación comprobando la interoperabilidad de los componentes del servidor recién instalados.

### <a name="grant-sharepoint-permissions-to-workbook-users"></a>Conceder permisos de SharePoint a los usuarios del libro
 Los usuarios necesitarán permisos de SharePoint para poder publicar o ver los libros. Asegúrese de conceder permisos de **vista** a los usuarios que necesiten ver los libros publicados y **contribuir** a los usuarios que publican o administran libros. Debe ser administrador de la colección de sitios para conceder permisos.

1.  En el sitio, haga clic en **acciones del sitio**.

2.  Haga clic en **permisos del sitio**.

3.  Cree grupos según sea necesario si desea que haya un conjunto de usuarios con permisos **Contribuir** y otro grupo para un conjunto de usuarios que solo tengan permisos **Ver** .

4.  Escriba las cuentas de usuario de dominio o de grupo de Windows que deben tener pertenencia a grupos. En este caso, no use direcciones de correo electrónico ni grupos de distribución si la aplicación está configurada para la autenticación clásica.

### <a name="install-adonet-data-services-35-sp1"></a>Instalar ADO.NET Data Services 3.5 SP1
 ADO.NET Data Services se requiere para exportar fuentes de distribución de datos de las listas de SharePoint. SharePoint 2010 no incluye este componente en el programa PrerequisiteInstaller, de modo que debe instalarlo manualmente.

1.  Vaya a la documentación sobre los requisitos de hardware y software para SharePoint 2010, [determinar los requisitos de hardware y software (SharePoint 2010)](https://go.microsoft.com/fwlink/?LinkId=169734)

2.  En Instalar requisitos previos de software, busque el vínculo de ADO.NET Data Services 3.5 correspondiente al sistema operativo que está usando.

3.  Haga clic en el vínculo y ejecute el programa de instalación que instala el servicio.

### <a name="install-data-providers-used-in-data-refresh-and-check-user-permissions"></a>Proveedores de datos de configuración utilizados en los permisos de actualización de datos y comprobación de usuario
 La actualización de datos del lado servidor permite a los usuarios reimportar los datos actualizados en sus libros en modo desatendido. Para que la actualización de datos se realice correctamente, el servidor debe tener el mismo proveedor de datos que se usó para importar originalmente los datos. Además, la cuenta de usuario en la que se ejecuta la actualización de datos requiere a menudo permisos de lectura en los orígenes de datos externos. Asegúrese de comprobar los requisitos para habilitar y configurar la actualización de datos a fin de garantizar que el resultado es correcto. Para obtener más información, vea [actualización de datos PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md).

### <a name="change-application-pool-and-service-identities-in-sharepoint"></a>Cambiar el grupo de aplicaciones y las identidades de servicio en SharePoint
 La herramienta de configuración de PowerPivot aprovisiona características de granja, aplicaciones y servicios para que se ejecuten bajo una cuenta única. Así se simplifica la instalación, pero la implementación resultante no cumple los requisitos de seguridad de una granja de SharePoint. Para crear una implementación más sólida, cambie los grupos de aplicaciones y las identidades de servicio de forma que se ejecuten bajo cuentas diferentes cuando la instalación se haya completado. Para obtener más información, vea [configurar las cuentas de servicio PowerPivot](power-pivot-sharepoint/configure-power-pivot-service-accounts.md).

### <a name="create-additional-trusted-sites-in-excel-services"></a>Crear sitios de confianza adicionales en Excel Services
 Puede agregar sitios de confianza en Excel Services para cambiar los permisos y la configuración de los sitios que proporcionan libros de Excel y datos PowerPivot. Para obtener más información, consulte [Create a trusted location for PowerPivot sites in Central Administration](power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).

### <a name="add-servers-or-applications"></a>Agregar servidores o aplicaciones
 Con el tiempo, si decide que se necesitan mayores capacidades de almacenamiento y procesamiento de datos, puede agregar una segunda instancia de PowerPivot para SharePoint a la granja. Para obtener instrucciones, consulte [lista de comprobación de implementación: escalado horizontal mediante la adición de servidores de PowerPivot a una granja de servidores de SharePoint 2010](../../2014/sql-server/install/deployment-checklist-scale-out-adding-powerpivot-servers-sharepoint-2010-farm.md).

## <a name="additional-resources"></a>Recursos adicionales
 La ![configuración de SharePoint](media/as-sharepoint2013-settings-gear.gif "Configuración de SharePoint") [envía comentarios e información de contacto a través de Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).

## <a name="see-also"></a>Consulte también
 [PowerPivot Configuration Tools](power-pivot-sharepoint/power-pivot-configuration-tools.md) [Configuración y administración de PowerPivot herramientas de configuración PowerPivot en administración central](power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)


