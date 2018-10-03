---
title: Actualización de datos PowerPivot con SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 01b54e6f-66e5-485c-acaa-3f9aa53119c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1af27b0571ef073a5ada2937b93b6cc0487974d8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143753"
---
# <a name="powerpivot-data-refresh-with-sharepoint-2010"></a>Actualización de datos PowerPivot con SharePoint 2010
  La actualización de datos [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] es una operación del lado servidor programada que consulta orígenes de datos externos para actualizar datos [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] incrustados en un libro de Excel 2010 almacenado en una biblioteca de contenido.  
  
 La actualización de datos es una característica integrada de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] para SharePoint, pero su uso requiere la ejecución de servicios y trabajos de temporizador específicos en la granja de SharePoint 2010. A menudo, para que la actualización de datos se realice correctamente, suelen requerirse procedimientos de administración adicionales, como la instalación de proveedores de datos y la comprobación de permisos de base de datos.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]**  SharePoint 2010  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] y SharePoint Server 2013 Excel Services usan una arquitectura diferente para la actualización de datos de [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] modelos de datos. La nueva arquitectura emplea Excel Services como componente principal para cargar modelos de datos de PowerPivot. La arquitectura usada anteriormente para la actualización de datos se basaba en un servidor que ejecutaba el Servicio de sistema de PowerPivot y [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en modo de SharePoint para cargar los modelos de datos. Para obtener más información, consulte [actualización de datos de PowerPivot con SharePoint 2013](power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md).  
  
 **En este tema:**  
  
 [Paso 1: Habilitar el servicio Store seguro y generar una clave maestra](#bkmk_services)  
  
 [Paso 2: Desactivar opciones de credenciales que no desea admitir](#bkmk_creds)  
  
 [Paso 3: Creación de aplicaciones de destino para almacenar las credenciales usadas en la actualización de datos](#bkmk_stored)  
  
 [Paso 4: Configurar el servidor de actualización de datos escalables](#bkmk_scale)  
  
 [Paso 5: Instalar a los proveedores de datos utilizados para importar datos de PowerPivot](#bkmk_installdp)  
  
 [Paso 6: Conceder permisos para crear programaciones y acceder a orígenes de datos externos](#bkmk_accounts)  
  
 [Paso 7: Habilitar la actualización del libro para la actualización de datos](#bkmk_upgradewrkbk)  
  
 [Paso 8: Comprobar la configuración de actualización de datos](#bkmk_verify)  
  
 [Modificar la configuración de actualización de datos](#bkmk_config)  
  
 [Volver a programar el trabajo del temporizador de actualización de datos PowerPivot](#configTimerJob)  
  
 [Deshabilitar el trabajo de temporizador de actualización de datos](#bkmk_disableDR)  
  
 Cuando se haya asegurado de que los permisos y el entorno del servidor están configurados, la actualización de datos estará lista para usarse. Para usar una actualización de datos, el usuario de SharePoint crea una programación en un libro PowerPivot que especifica con qué frecuencia se produce la actualización de datos. La creación de la programación suele realizarla el propietario del libro o el autor que publica el archivo en SharePoint. Esta persona crea y administra las programaciones de la actualización de datos para los libros que posee. Para obtener más información, consulte [programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
##  <a name="bkmk_services"></a> Paso 1: Habilitar el servicio Store seguro y generar una clave maestra  
 La actualización de datos PowerPivot depende de Servicio de almacenamiento seguro para proporcionar las credenciales que se utilizan para ejecutar trabajos de actualización de datos y conectarse a orígenes de datos externos que utilizan credenciales almacenadas.  
  
 Si instaló PowerPivot para SharePoint utilizando la opción Nuevo servidor, el Servicio de almacenamiento seguro se configura automáticamente. En todos los demás escenarios de instalación, debe crear y configurar una aplicación de servicio y generar una clave de cifrado maestra para el Servicio de almacenamiento seguro.  
  
> [!NOTE]  
>  Para configurar el Servicio de almacenamiento seguro o delegar la administración de dicho servicio a otro usuario, debe ser el administrador de una granja. Para establecer o modificar la configuración, una vez habilitada, debe ser el administrador de una aplicación de servicio.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  En la cinta de opciones de las aplicaciones de servicio, en crear, haga clic en **New**.  
  
3.  Seleccione **servicio Store seguro**.  
  
4.  En el **crear aplicación de Store seguro** , escriba un nombre para la aplicación.  
  
5.  En **base de datos**, especifique la instancia de SQL Server que hospedará la base de datos para esta aplicación de servicio. El valor predeterminado es la instancia del motor de base de datos de SQL Server que hospeda las bases de datos de configuración de la granja.  
  
6.  En **nombre de base de datos**, escriba el nombre de la base de datos de aplicación de servicio. El valor predeterminado es Secure_Store_Service_DB_\<guid >. El nombre predeterminado corresponde al de la aplicación de servicio. Si escribió un nombre de aplicación del servicio único, siga una convención de nomenclatura similar para el nombre de la base de datos, de modo que pueda administrarlos juntos.  
  
7.  En **Autenticación de bases de datos**, el valor predeterminado es Autenticación de Windows. Si elige Authentication SQL, consulte la guía de administrador de SharePoint para obtener información sobre cómo utilizar el tipo de autenticación en la granja.  
  
8.  En el grupo de aplicaciones, seleccione **crear nuevo grupo de aplicaciones.** Especifique un nombre descriptivo que ayudará a otros administradores del servidor a identificar cómo se utiliza el grupo de aplicaciones.  
  
9. Seleccione una cuenta de seguridad para el grupo de aplicaciones. Especifique una cuenta administrada para utilizar una cuenta de usuario de dominio.  
  
10. Acepte los valores predeterminados restantes y, a continuación, haga clic en **Aceptar.** La aplicación de servicio aparecerá junto a otros servicios administrados en la lista de aplicaciones de servicio de la granja de servidores.  
  
11. Haga clic en la aplicación Servicio de almacenamiento seguro en la lista.  
  
12. En la cinta de opciones de las aplicaciones de servicio, haga clic en **administrar**.  
  
13. En administración de claves, haga clic en **generar nueva clave**.  
  
14. Especifique y confirme una frase de contraseña. La frase de contraseña se utilizará para agregar más aplicaciones de servicio compartidas del almacén seguro.  
  
15. Haga clic en **Aceptar**.  
  
 Para que esté disponible el registro de auditoría de las operaciones del Servicio de almacenamiento, que se utiliza para solucionar problemas, es necesario habilitarlo antes. Para obtener más información acerca de cómo habilitar el registro, consulte [configurar Secure Store Service (SharePoint 2010)](http://go.microsoft.com/fwlink/p/?LinkID=223294).  
  
##  <a name="bkmk_creds"></a> Paso 2: Desactivar opciones de credenciales que no desea admitir  
 La actualización de datos PowerPivot proporciona tres opciones de credencial en una programación de actualización de datos. Cuando el propietario de un libro programa una actualización de datos, elige una de estas opciones, que determinan la cuenta en la que se ejecutará el trabajo de actualización de datos. Como administrador, puede determinar qué opciones de credencial estarán disponibles para los propietarios de las programaciones.  
  
 Debe tener como mínimo una opción disponible para que la actualización de datos funcione.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 Opción 1, **configurada por el Administrador de cuenta de actualización de los datos de uso**, siempre aparece en la página de definición de programación, pero solo funciona si se configura la cuenta de actualización de datos desatendida. Para obtener más información sobre cómo crear la cuenta, consulte [configurar la cuenta de actualización de datos desatendida de PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
 Opción 2, **conectar con las credenciales de windows siguiente**, siempre aparece en la página, pero solo funciona cuando se habilita la **permiten a los usuarios especificar credenciales de Windows personalizadas** opción en el servicio página de configuración de la aplicación. Esta opción está habilitada de forma predeterminada, pero puede deshabilitarla si los inconvenientes de utilizarla superan a las ventajas (vea más abajo).  
  
 Opción 3, **conectar con las credenciales guardadas en el servicio Store seguro**, siempre aparece en la página, pero solo funciona cuando el propietario de una programación proporciona una aplicación de destino válido. Un administrador debe crear de antemano estas aplicaciones de destino y proporcionar después el nombre de aplicación a los creadores de las programaciones de actualización de datos. Para obtener más información sobre cómo crear una aplicación de destino para los datos de las operaciones de actualización, vea [configurar las credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
 **Configurar la opción de credencial 2, "Conectar con las siguientes credenciales de usuario de Windows"**  
  
 La aplicación de servicio PowerPivot incluyen una opción de credencial que permite a los propietarios de las programaciones escribir un nombre de usuario y una contraseña de Windows arbitrarios para ejecutar un trabajo de actualización de datos. Esta es la segunda opción de credencial de la página de definición de la programación:  
  
 ![SSAS_PPS_ScheduleDataRefreshCreds](media/ssas-pps-scheduledatarefreshcreds.gif "SSAS_PPS_ScheduleDataRefreshCreds")  
  
 Esta opción de credencial se habilita de forma predeterminada. Cuando se habilite esta opción de credencial, el Servicio de sistema de PowerPivot generará una aplicación de destino en el Servicio de almacenamiento seguro para almacenar el nombre de usuario y la contraseña especificados por el propietario de la programación. Se crea una aplicación de destino generada con esta convención de nomenclatura: PowerPivotDataRefresh_\<guid >. Las aplicaciones de destino se crean para cada conjunto de credenciales de Windows. Si ya existe una aplicación de destino que es propiedad del Servicio de sistema PowerPivot y almacena el nombre de usuario y la contraseña especificados por la persona que ha definido la programación, el Servicio de sistema de PowerPivot utilizará esa aplicación de destino en lugar de crear otra.  
  
 La principal ventaja de utilizar esta opción de credencial es la facilidad de uso y la simplicidad. El trabajo previo es mínimo porque las aplicaciones de destino ya están creadas. Además, al ejecutar la actualización de datos con las credenciales del propietario de la programación (que probablemente es la persona que creó el libro), también, se simplifica el nivel inferior de los requisitos de permiso. Probablemente, este usuario ya tiene los permisos de la base de datos de destino. Cuando la actualización de datos se ejecute con la identidad de usuario de Windows de esta persona, cualquier conexión de datos que especifique 'usuario actual' funcionará automáticamente.  
  
 La desventaja es la limitación de la capacidad de administración. Aunque las aplicaciones de destino se crean automáticamente, no se eliminan del mismo modo ni se actualizan cuando cambia la información de la cuenta. Las directivas de expiración de contraseñas pueden hacer que estas aplicaciones de destino queden desfasadas. Los trabajos de actualización de datos que utilicen credenciales caducadas empezarán a producir errores. Cuando suceda esto, los propietarios de las programaciones tendrán que actualizar sus credenciales proporcionando los valores actuales de nombre de usuario y contraseña en una programación de actualización de datos. En ese punto se creará una nueva aplicación de destino. Con el tiempo, a medida que los usuarios agreguen y revisen la información de credenciales en sus programas de actualización de datos, puede encontrarse con un número enorme de aplicaciones de destino generadas automáticamente en su sistema.  
  
 Actualmente, no hay ningún modo de determinar cuáles de estas aplicaciones de destino están activas o inactivas ni de seguir una aplicación de destino concreta hasta las programaciones de actualización de datos que la utilizan. En general, debe dejar las aplicaciones de destino tal cual, porque si las eliminara podría interrumpir las programaciones de actualización de datos existentes. La eliminación de una aplicación de destino que todavía esté en uso puede hacer que la actualización de datos produzca un error y aparezca el mensaje "No se encontró la aplicación de destino" en la página del historial de actualización de datos del libro.  
  
 Si opta por deshabilitar esta opción de credencial, podrá eliminar todas las aplicaciones de destino que se generaron para la actualización de datos de PowerPivot sin ningún riesgo.  
  
 **Deshabilitar el uso de credenciales de Windows arbitrarias en programaciones de actualización de datos**  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en el nombre de la aplicación de servicio PowerPivot. Se muestra el Panel de administración de PowerPivot.  
  
3.  En acciones, haga clic en **configurar las opciones de la aplicación de servicio** para abrir la página de configuración de aplicación de servicio PowerPivot  
  
4.  En la sección de actualización de datos, desactive la **permiten a los usuarios especificar credenciales de Windows personalizadas** casilla de verificación.  
  
     ![SSAS_PowerPivotDatarefreshOptions_AllowUser](media/ssas-powerpivotdatarefreshoptions-allowuser.gif "SSAS_PowerPivotDatarefreshOptions_AllowUser")  
  
##  <a name="bkmk_stored"></a> Paso 3: Creación de aplicaciones de destino para almacenar las credenciales usadas en la actualización de datos  
 Una vez configurado el Servicio de almacenamiento seguro, los administradores de SharePoint pueden crear aplicaciones de destino para que las credenciales almacenadas estén disponibles con fines de actualización de datos, incluida la cuenta de actualización de datos desatendida de PowerPivot o cualquier otra cuenta que se utilice para ejecutar el trabajo o conectar con orígenes de datos externos.  
  
 Recuerde, como se señaló en la sección anterior, que tiene que crear aplicaciones de destino para que puedan utilizarse determinadas opciones de credencial. Concretamente, debe crear aplicaciones de destino para la cuenta de actualización de datos desatendida de PowerPivot, además de cualquier otra credencial almacenada que considere que es probable que se utilice en las operaciones de actualización de datos.  
  
 Para obtener más información sobre cómo crear aplicaciones de destino que contengan las credenciales almacenadas, vea [configurar la cuenta de actualización de datos desatendida de PowerPivot &#40;PowerPivot para SharePoint&#41; ](configure-unattended-data-refresh-account-powerpivot-sharepoint.md) y [ Configurar credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
##  <a name="bkmk_scale"></a> Paso 4: Configurar el servidor de actualización de datos escalables  
 De forma predeterminada, las instalaciones de PowerPivot para SharePoint admiten consultas a petición y actualizaciones de datos programadas.  
  
 Puede especificar para cada instalación si la instancia de servidor de Analysis Services admitirá consultas y actualizaciones de datos programadas o estará dedicada a una clase concreta de operación. Si tiene varias instalaciones de PowerPivot para SharePoint en su granja, podría plantearse dedicar un servidor exclusivamente para las operaciones de actualización de datos si encuentra que los trabajos se retrasan o producen errores.  
  
 Además, si el hardware subyacente lo admite, puede aumentar el número de trabajos de actualización de datos que se ejecutan en paralelo. De forma predeterminada, el número de trabajos que se pueden ejecutar en paralelo se calcula en función de la memoria del sistema, pero se puede aumentar si se tiene más capacidad de CPU para admitir la carga de trabajo.  
  
 Para obtener más información, consulte [Configurar actualización de datos dedicada o procesamiento Query-Only &#40;PowerPivot para SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md).  
  
##  <a name="bkmk_installdp"></a> Paso 5: Instalar a los proveedores de datos utilizados para importar datos de PowerPivot  
 Una operación de actualización de datos es esencialmente la repetición de una operación de importación que recuperó los datos originales. Esto significa que los mismos proveedores de datos utilizados para importar los datos en la aplicación cliente PowerPivot deben estar instalados en el servidor PowerPivot.  
  
 Debe ser administrador local para instalar los proveedores de datos en un servidor de Windows. Si instala controladores adicionales, asegúrese de instalarlos en cada equipo de la granja de SharePoint que tenga PowerPivot para SharePoint instalado. Si tiene varios servidores de PowerPivot en la granja, debe instalar los proveedores en cada uno de ellos.  
  
 Recuerde que los servidores de SharePoint son aplicaciones de 64 bits. Asegúrese de instalar la versión de 64 bits de los proveedores de datos que usa para que admitan las operaciones de actualización de datos.  
  
##  <a name="bkmk_accounts"></a> Paso 6: Conceder permisos para crear programaciones y acceder a orígenes de datos externos  
 Los propietarios o los autores de los libros deben tener el permiso para **contribuir** si desean programar la actualización de los datos en un libro. Dado este nivel de permisos, pueden abrir y modificar la página de configuración de la actualización de datos del libro para especificar las credenciales y la información de programación que se usa para actualizar los datos.  
  
 Además de los permisos de SharePoint, también se deben revisar los permisos de base de datos de los orígenes de datos externos para asegurarse de que las cuentas utilizadas durante la actualización de datos tengan suficientes derechos de acceso a los datos. La determinación de los requisitos de permiso requerirá una evaluación cuidadosa por su parte porque los permisos que necesita conceder variarán en función de la cadena de conexión del libro y la identidad del usuario con la que se está ejecutando el trabajo de actualización de datos.  
  
 **¿Por qué importan cadenas de conexión existentes en un libro de PowerPivot para las operaciones de actualización de datos de PowerPivot**  
  
 Cuando se ejecuta la actualización de datos, el servidor envía una solicitud de conexión al origen de datos externo utilizando la cadena de conexión que se creó cuando se importaron originalmente los datos. La ubicación del servidor, el nombre de base de datos y los parámetros de autenticación especificados en esa cadena de conexión se vuelven a utilizar durante la actualización de datos para acceder a los mismos orígenes de datos. La cadena de conexión y su construcción general no se pueden modificar para la actualización de datos. Simplemente se vuelve a actualizar tal cual durante la actualización de datos. En algunos casos, si va a utilizar una autenticación diferente a la de Windows para conectarse a un origen de datos, puede reemplazar el nombre de usuario y la contraseña en la cadena de conexión. Se proporciona más información sobre esto más adelante en este tema.  
  
 Para la mayoría de los libros, la opción de autenticación predeterminada de la conexión es utilizar conexiones de confianza o la seguridad integrada de Windows, lo que produce cadenas de conexión que incluyen `SSPI=IntegratedSecurity` o `SSPI=TrustedConnection`. Cuando esta cadena de conexión se utiliza durante la actualización de datos, la cuenta utilizada para ejecutar el trabajo de actualización de datos se convierte en el 'usuario actual.' Como tal, esta cuenta necesitará permisos de lectura en cualquier origen de datos externo al que se acceda a través de una conexión de confianza.  
  
 **¿Ha habilitado la PowerPivot cuenta de actualización de datos desatendida?**  
  
 Si la respuesta es sí, debe otorgar esos permisos de lectura de la cuenta en los orígenes de datos a los que se accede durante la actualización de datos. El motivo por el que esta cuenta necesita permisos de lectura es porque en un libro que utilice las opciones de autenticación predeterminado, la cuenta desatendida será el 'usuario actual' durante la actualización de datos. A menos que el propietario de la programación invalide las credenciales en la cadena de conexión, esta cuenta necesitará permisos de lectura en todos los orígenes de datos que se utilicen de forma activa en una organización.  
  
 **¿Está utilizando la opción de credencial 2: permitir que el propietario de la programación que escriba un nombre de usuario de Windows y una contraseña?**  
  
 Normalmente, los usuarios que crean libros PowerPivot ya tienen suficientes permisos porque importaron los datos en primer lugar. Si estos usuarios configuran posteriormente la actualización de datos para ejecutarse con su propia identidad de usuario de Windows, se utilizará su cuenta de usuario de Windows, que ya posee derechos sobre la base de datos, para recuperar datos durante la actualización de datos. Los permisos existentes deberían ser suficientes.  
  
 **¿Está utilizando la opción de credencial 3: uso de una aplicación de destino del servicio Store seguro para proporcionar una identidad de usuario para ejecutar trabajos de actualización de datos?**  
  
 Todas las cuentas que se utilicen para ejecutar un trabajo de la actualización de datos necesitan permisos de lectura, por los mismas motivos que los descritos para la cuenta de la actualización de datos desatendida de PowerPivot.  
  
 **Cómo comprobar las cadenas de conexión para determinar si pueden invalidar las credenciales utilizadas durante la actualización de datos**  
  
 Como se indicó anteriormente, podrá sustituir el nombre de usuario y la contraseña en el nivel de trabajo de actualización de datos si la conexión utiliza una autenticación diferente a la de Windows (por ejemplo, la autenticación de SQL Server). Las credenciales diferentes a la de Windows se pasan a la cadena de conexión utilizando los parámetros de identificador de usuario y contraseña. Si el libro contiene una cadena de conexión con estos parámetros, también puede especificar un nombre de usuario y una contraseña diferentes para actualizar los datos procedentes de ese origen de datos.  
  
 Los siguientes pasos explican cómo determinar si tiene una cadena de conexión que acepta invalidaciones de nombre de usuario y contraseña.  
  
1.  Abra el libro en Excel.  
  
2.  Abra la ventana de PowerPivot (en Excel, en la cinta de opciones de PowerPivot, haga clic en la ventana de PowerPivot).  
  
3.  Haga clic en **diseño**.  
  
4.  Haga clic en **las conexiones existentes**.  
  
     Todas las conexiones que se usan en el libro se muestran bajo **conexiones de datos PowerPivot**.  
  
5.  Seleccione la conexión y haga clic en **editar**y, a continuación, haga clic en **avanzadas**. La cadena de conexión se encuentra en la parte inferior de la página.  
  
 Si ve **Integrated Security = SSPI** en la cadena de conexión no puede invalidar las credenciales en la cadena de conexión. La conexión siempre utilizará al usuario actual. Se omitirá cualquier credencial que proporcione.  
  
 Si ve **Persist Security Info = False, Password =\* \* \* \* \* \* \* \* \* \* \*, UserID =\<userlogin >**, tendrá una cadena de conexión que aceptará invalidaciones de credenciales. Las credenciales que aparecen en una cadena de conexión (como las de identificación de usuario y contraseña) no son credenciales de Windows, sino que son inicios de sesión de base de datos u otras cuentas de inicio de sesión válidos para el origen de datos de destino.  
  
 **Cómo invalidar credenciales en la cadena de conexión**  
  
 Para invalidar credenciales, especifique las credenciales de origen de datos en la programación de actualización de datos. Como administrador, puede proporcionar una aplicación de destino en el Servicio de almacenamiento seguro que asigne las credenciales usadas para acceder a los datos externos. El propietario de la programación puede especificar el identificador de la aplicación de destino en la programación de la actualización de datos que defina. Para obtener más información acerca de cómo crear esta aplicación de destino, vea [configurar las credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
 También, el propietario de la programación puede escribir en el conjunto de credenciales que se utilizan para conectar a los orígenes de datos durante la actualización de datos. La siguiente ilustración muestra esta opción de origen de datos en la página de definición de la programación.  
  
 ![SSAS_PowerPivotKJ_DataRefreshDSOptions](media/ssas-powerpivotkj-datarefreshdsoptions.gif "SSAS_PowerPivotKJ_DataRefreshDSOptions")  
  
 **Identificar los requisitos de acceso de datos**  
  
 Como se ha indicado en secciones anteriores, la cuenta utilizada para ejecutar la actualización de datos y conectarse a los orígenes de datos externos suele ser una y la misma. Por tanto, el conjunto de opciones establecidas en esta parte de la página de programación de actualización de datos determina la cuenta que se utilizará para acceder a los orígenes de datos externos. Esta podría ser la cuenta de la actualización de datos desatendida de PowerPivot, la cuenta de Windows de un usuario individual, o la cuenta almacenada en una aplicación de destino predefinida.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 En los casos en que la cuenta utilizada para ejecutar la actualización de datos no coincida con la cuenta para importar datos (por ejemplo, la cuenta de la actualización de datos desatendida de PowerPivot mediante la opción de credencial uno, o algún otro conjunto de credenciales almacenadas mediante la opción de credencial tres), necesitará crear un nuevo inicio de sesión de base de datos para esa cuenta y concederle permisos de lectura en los orígenes de datos externos.  
  
 Cuando conozca qué cuentas requieren acceso a datos, empiece a comprobar los permisos en los orígenes de datos que se utilizan con mayor frecuencia en los libros PowerPivot. Comience con cualquier almacenamiento de datos o base de datos de informes que se utilice activamente, pero solicite también a sus usuarios de PowerPivot más activos que introduzcan datos para averiguar qué orígenes de datos están utilizando. Cuando tenga una lista de orígenes de datos, podrá empezar a comprobar cada uno de ellos para asegurarse de que se establecen correctamente los permisos.  
  
##  <a name="bkmk_upgradewrkbk"></a> Paso 7: Habilitar la actualización del libro para la actualización de datos  
 De forma predeterminada, los libros creados con la versión de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] de PowerPivot para Excel no se pueden configurar para la actualización de datos programada en una versión de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] de PowerPivot para SharePoint. Si hospeda versiones de los libros PowerPivot más recientes y antiguas en el entorno de SharePoint, debe actualizar cualquier libro [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] para poder programarlos para la actualización automática de los datos en el servidor.  
  
##  <a name="bkmk_verify"></a> Paso 8: Comprobar la configuración de actualización de datos  
 Para comprobar la actualización de datos, debe tener un libro PowerPivot publicado en un sitio de SharePoint. Debe tener permisos para contribuir en el libro y para acceder a los orígenes de datos que estén incluidos en el programa de actualización de datos.  
  
 Al crear la programación, seleccione el **también actualizar lo más rápido posible** casilla de verificación para ejecutar la actualización de datos inmediatamente. A continuación, puede comprobar la página del historial de actualización de datos de ese libro para comprobar que se ejecutó correctamente. Recuerde que el trabajo del temporizador de actualización de datos PowerPivot se ejecuta cada minuto. La obtención de la confirmación de que la actualización de datos finalizó correctamente tardará como mínimo ese tiempo.  
  
 Asegúrese de probar todas las opciones de credencial que tiene previsto admitir. Por ejemplo, si configuró la cuenta de la actualización de datos desatendida de PowerPivot, compruebe que la actualización de datos finalice correctamente utilizando esa opción. Para obtener más información sobre cómo programar y ver la información de estado, vea [programar una actualización de datos &#40;PowerPivot para SharePoint&#41; ](schedule-a-data-refresh-powerpivot-for-sharepoint.md) y [historial de actualización de datos de vista &#40;PowerPivot para SharePoint &#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
 Si se produce un error de actualización de datos, consulte el [Troubleshooting PowerPivot Data Refresh](http://go.microsoft.com/fwlink/?LinkID=223279) página wiki de TechNet para hallar posibles soluciones.  
  
##  <a name="bkmk_config"></a> Modificar la configuración de actualización de datos  
 Cada aplicación de servicio PowerPivot tiene valores de configuración que afectan a las operaciones de actualización de datos. En esta sección se explica cómo modificar dichos valores.  
  
###  <a name="procIntervals"></a> Establezca "Business Hours" para determinar las horas de trabajo de procesamiento  
 Los usuarios de SharePoint que programan las operaciones de actualización de datos pueden especificar una hora de inicio anterior a "Después del horario comercial". Esto puede ser útil si desean recuperar datos de transacciones comerciales que se hayan acumulado durante el día. Como administrador de una granja, puede especificar el intervalo de horas que mejor define un día laboral en una organización. Si define el día laboral como de 04:00 a 20:00 horas, el procesamiento de las actualizaciones de datos que se base en una hora de inicio "Después del horario comercial" comenzará a las 20:01.  
  
 Las solicitudes de actualización de datos que se ejecutan durante horas de poca actividad se agregan a la cola en el orden en el que se recibe la solicitud. Las solicitudes individuales se procesarán a medida que los recursos del servidor estén disponibles.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en el nombre de la aplicación de servicio PowerPivot. Se muestra el Panel de administración de PowerPivot.  
  
3.  En acciones, haga clic en **configurar las opciones de la aplicación de servicio** para abrir la página de configuración de aplicación de servicio PowerPivot  
  
4.  En la sección Actualización de datos, en Horario comercial, escriba una hora de inicio y una hora de finalización que defina el período de procesamiento en un horario posterior al comercial.  
  
     Si no desea definir un período de procesamiento en horas de poca actividad, puede especificar el mismo valor en Hora de inicio y en Hora de finalización (por ejemplo, 12:00 para ambas). Sin embargo, sea consciente de que las páginas de definición de la programación de los sitios de SharePoint seguirán manteniendo como opción "Después del horario comercial". Los usuarios que seleccionen esa opción en una granja que no tenga definido un intervalo de procesamiento en horas de poca actividad obtendrán a la larga errores en la actualización de datos porque los trabajos de procesamiento no podrán iniciarse.  
  
5.  Haga clic en **Aceptar**.  
  
###  <a name="usagehist"></a> Limitar cuánto tiempo se conserva el historial de actualización de datos  
 El historial de la actualización de datos es un registro detallado de los mensajes de error y de éxito que se generan con el tiempo para las operaciones de actualización de datos. La información del historial se recopila y administra a través del sistema de recopilación de datos de uso en la granja. Por tanto, los límites que establezca en el historial de datos de uso también se aplicarán al historial de la actualización de datos. Dado que los informes de actividad de uso reúnen datos de todo el sistema de PowerPivot, se usa una sola configuración del historial para controlar la retención de los datos tanto para el historial de actualización de datos como para todos los demás datos de uso que se recopilan y almacenan.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en el nombre de la aplicación de servicio PowerPivot. Se muestra el Panel de administración de PowerPivot.  
  
3.  En acciones, haga clic en **configurar las opciones de la aplicación de servicio** para abrir la página de configuración de aplicación de servicio PowerPivot  
  
4.  En la sección de recopilación de datos de uso, en Historial de datos de uso, escriba el número de días para los que desea mantener un registro de actividad de la actualización de datos para cada libro.  
  
     El valor predeterminado es 365 días. El valor mínimo es 1 día y el valor máximo es 5000 días. 0 especifica un período de retención ilimitado; los datos nunca se eliminan. Observe que no hay ningún valor para desactivar el historial.  
  
5.  Haga clic en **Aceptar**.  
  
 La información del historial se pone a disposición de los usuarios de SharePoint cuando eligen la opción Administrar actualización de datos en un libro que tiene un historial de actualización de datos. Esta información también se utiliza en el Panel de administraciones de PowerPivot que usan los administradores de una granja para administrar las operaciones de servicio PowerPivot. Para obtener más información, consulte [historial de actualización de datos de vista &#40;PowerPivot para SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
 El almacenamiento físico a largo plazo de datos del historial está en la base de datos de aplicación de servicio PowerPivot para la aplicación de servicio PowerPivot. Para obtener más información acerca de cómo se recopilan y almacenan los datos de uso, consulte [PowerPivot Usage Data Collection](power-pivot-sharepoint/power-pivot-usage-data-collection.md).  
  
##  <a name="configTimerJob"></a> Volver a programar el trabajo del temporizador de actualización de datos PowerPivot  
 Un trabajo de temporizador de actualización de datos PowerPivot que examina la información de programación en la base de datos de aplicación de servicio PowerPivot desencadena una actualización de datos programada en intervalos de un minuto. Cuando la actualización de datos se programa para iniciarse, el trabajo de temporizador agrega la solicitud a una cola de procesamiento en un servidor de PowerPivot disponible.  
  
 Puede aumentar el intervalo de tiempo entre análisis como técnica de ajuste del rendimiento. También puede deshabilitar el trabajo de temporizador para detener las operaciones de actualización de datos temporalmente mientras solucione problemas.  
  
 La configuración predeterminada es un minuto, que es el valor mínimo que se puede especificar. Se recomienda este valor porque proporciona el resultado más predecible para las programaciones que se ejecutan en momentos arbitrarios a lo largo del día. Por ejemplo, si un usuario programa la actualización de datos para las 4:15 p.m. y el trabajo de temporizador busca programaciones cada minuto, la solicitud de actualización de datos programada se detectará a las 4:15 y el procesamiento se producirá pocos minutos después de las 4:15.  
  
 Si aumenta el intervalo de exploración de modo que se ejecute con muy poca frecuencia (por ejemplo, una vez al día a medianoche), todas las operaciones de actualización de datos que se programen para ejecutarse durante ese intervalo se agregarán a la cola de procesamiento a la vez, con lo que se podría sobrecargar el servidor y privar a otras aplicaciones de los recursos del sistema. Según el número de actualizaciones programadas, la cola de procesamiento de las operaciones de actualización de datos podría aumentar hasta un punto en que no todos los trabajos puedan completarse. Las solicitudes de actualización de datos al final de la cola podrían quitarse si se ejecutaran en el intervalo de procesamiento siguiente.  
  
 Si el hardware lo admite, puede aliviar este problema especificando procesadores adicionales para ejecutar más trabajos de actualización de datos en paralelo. Para obtener más información, consulte [Configurar actualización de datos dedicada o procesamiento Query-Only &#40;PowerPivot para SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md). Para obtener más información acerca de cómo se detectan, agrega a una cola y procesa las solicitudes de actualización de datos, vea [PowerPivot Data Refresh](power-pivot-sharepoint/power-pivot-data-refresh.md).  
  
1.  En Administración central, haga clic en **Supervisión**.  
  
2.  Haga clic en **Revisar definiciones de trabajo**.  
  
3.  Seleccione el **trabajo de temporizador de actualización de datos PowerPivot**.  
  
4.  Modifique la frecuencia de programación para cambiar la frecuencia con que el trabajo de temporizador realiza los exámenes para obtener información de programación de la actualización de datos.  
  
##  <a name="bkmk_disableDR"></a> Deshabilitar el trabajo de temporizador de actualización de datos  
 El trabajo de temporizador de actualización de datos PowerPivot se realiza en el nivel de granja y se habilita o deshabilita para todas las instancias del servidor de PowerPivot de la granja. No está asociado a ninguna aplicación web ni a ninguna aplicación de servicio PowerPivot concretas. No puede deshabilitarlo en algunos servidores para obligar a que se procese la actualización de datos en otros servidores de la granja.  
  
 Si deshabilita el trabajo de temporizador de actualización de datos PowerPivot, las solicitudes que ya estaban en la cola se procesarán, pero no se agregará ninguna solicitud nueva hasta que vuelva a habilitar el trabajo. Las solicitudes que se programaran para producirse en el pasado no se procesan.  
  
 Deshabilitar el trabajo de temporizador no tiene ningún efecto en la disponibilidad de las características de las páginas de aplicación. No hay ninguna manera de quitar u ocultar la característica de actualización de datos en las aplicaciones web. Los usuarios que tengan permisos para contribuir o superiores todavía podrán crear nuevas programaciones para las operaciones de actualización de datos, aun cuando el trabajo de temporizador se deshabilite de forma permanente.  
  
## <a name="see-also"></a>Vea también  
 [Programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Configurar la actualización de datos dedicada o procesamiento de una sola consulta &#40;PowerPivot para SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)   
 [Configurar PowerPivot cuenta de actualización de datos desatendida &#40;PowerPivot para SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [Configurar credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
