---
title: Configurar la cuenta de actualización de datos desatendida de PowerPivot (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 81401eac-c619-4fad-ad3e-599e7a6f8493
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 894e7d4fb5a0234643cf237e767a8ae999e67496
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087422"
---
# <a name="configure-the-powerpivot-unattended-data-refresh-account-powerpivot-for-sharepoint"></a>Configurar la cuenta de actualización de datos desatendida de PowerPivot (PowerPivot para SharePoint)
  La cuenta de actualización de datos de PowerPoint desatendida es una cuenta designada para ejecutar trabajos de actualización de datos PowerPivot en una granja de SharePoint. Al configurarlo, se habilita la opción **usar la cuenta de actualización de datos configurada por el administrador** en una página de programación de actualización de datos (vea a continuación). Los autores de libros que programan la actualización de datos pueden elegir esta opción si desean utilizar la cuenta de actualización de datos desatendida de PowerPivot para ejecutar un trabajo de actualización de datos. Para obtener más información sobre cómo ver las opciones de credenciales en una programación de actualización de datos, vea [programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
 Según las opciones que seleccione al configurar el servidor, la cuenta de actualización de datos desatendida podría estar ya creada. En una configuración predeterminada, la identidad de la cuenta de actualización de datos desatendida se establece inicialmente en la cuenta de la granja. Puede mejorar la seguridad de la implementación cambiando la cuenta para que se ejecute como un usuario diferente. Siga estas instrucciones para cambiar la cuenta: [actualizar las credenciales que usa una cuenta de actualización de datos desatendida de PowerPivot existente](#bkmk_editUA).  
  
 En todos los demás escenarios de instalación, debe configurar esta cuenta manualmente siguiendo las instrucciones que aparecen a continuación.  
  
 Este tema contiene las siguientes secciones:  
  
 [Requisitos previos](#bkmk_prereq)  
  
 [Paso 1: crear una aplicación de destino y establecer las credenciales](#bkmk_create)  
  
 [Paso 2: especificar la cuenta desatendida en las páginas de configuración del servidor de PowerPivot](#bkmk_specifyUA)  
  
 [Paso 3: conceder permisos de contribución a la cuenta](#bkmk_grant)  
  
 [Paso 4: conceder permisos de lectura para tener acceso a los orígenes de datos externos utilizados en la actualización de datos](#bkmk_dbread)  
  
 [Paso 5: comprobar la disponibilidad de las cuentas en las páginas de configuración de la actualización de datos](#bkmk_verify)  
  
 [Usar la cuenta de actualización de datos PowerPivot desatendida.](#bkmk_use)  
  
 [Actualizar las credenciales utilizadas por una cuenta de actualización de datos desatendida de PowerPivot existente](#bkmk_editUA)  
  
##  <a name="prerequisites"></a><a name="bkmk_prereq"></a> Requisitos previos  
 El Servicio de almacenamiento seguro debe estar habilitado y configurado, y debe generarse una clave maestra. Para obtener instrucciones sobre cómo hacerlo, vea [actualización de datos PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
 Debe decidir de antemano la cuenta de usuario de dominio de Windows que se va a usar como cuenta de actualización de datos desatendida de PowerPivot. Debe ser una cuenta que se cree específicamente con este fin para que pueda supervisar cómo se usa.  
  
 Debe conocer la identidad de aplicación del Servicio de sistema de PowerPivot. Asignará a esta cuenta de servicio permisos de **control total** sobre la cuenta de actualización de datos desatendida cuando cree la aplicación de destino para ella en el paso 1. Estos permisos permiten al Servicio de sistema de PowerPivot recuperar las credenciales de la cuenta de actualización de datos desatendida durante la actualización de datos. Para obtener la información necesaria de la cuenta de servicio, abra la página **configurar cuentas de servicio** en administración central y seleccione el grupo de aplicaciones de servicio que usa la aplicación de servicio PowerPivot. De forma predeterminada, es el **grupo de aplicaciones de servicio: sistema de servicios Web de SharePoint**.  
  
## <a name="configure-the-unattended-powerpivot-data-refresh-account"></a>Configurar la cuenta de actualización de datos PowerPivot desatendida  
 Puede configurar solo una cuenta de actualización de datos desatendida de PowerPivot para cada aplicación de servicio PowerPivot. La información de la cuenta se almacena en el servicio de almacenamiento seguro en una aplicación de destino que se establece en una cuenta de usuario de dominio predefinida de Windows. Una vez creada la aplicación, puede especificarla como la cuenta de actualización de datos PowerPivot en las páginas de configuración de una aplicación de servicio PowerPivot.  
  
> [!NOTE]  
>  Cuando se realice la actualización de datos en la cuenta de actualización de datos desatendida, el informe de uso y el historial de actualización de datos se registran en la cuenta de usuario de Windows usada para la actualización de datos desatendida. Si necesita un registro más preciso de los individuos que solicitan la actualización de datos o que son los propietarios de las programaciones, considere una de las otras opciones para ejecutar la actualización de datos. Pedir a los usuarios que especifiquen sus propias credenciales (este es el valor predeterminado) o crear aplicaciones de destino adicionales para almacenar las credenciales de Windows que desee usar con fines de actualización de datos. Para obtener más información, vea [configurar credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
 Existen cinco pasos para crear la cuenta de actualización de datos desatendida.  
  
-   Cree una aplicación de destino en el servicio de almacenamiento seguro para la cuenta y especifique las credenciales.  
  
-   Especifique el identificador de la aplicación de destino para la cuenta de actualización de datos desatendida en la página de configuración del servidor PowerPivot.  
  
-   Conceda permisos de contribución a la cuenta.  
  
-   Conceda permisos de lectura a la cuenta para tener acceso a los orígenes de datos externos durante la actualización de datos.  
  
-   Compruebe que la cuenta esté disponible en la página de programación Administrar actualización de datos para un libro PowerPivot publicado.  
  
###  <a name="step-1-create-a-target-application-and-set-the-credentials"></a><a name="bkmk_create"></a>Paso 1: crear una aplicación de destino y establecer las credenciales  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en **servicio de almacenamiento seguro**.  
  
3.  En administrar aplicaciones de destino, haga clic en **nuevo**.  
  
4.  En identificador de la aplicación de destino, escriba **PowerPivotDataRefresh**.  
  
5.  En nombre para mostrar, escriba **actualización de datos PowerPivot**.  
  
6.  En Correo electrónico de contacto, escriba su dirección de correo electrónico.  
  
7.  En tipo de aplicación de destino, seleccione **individual**.  
  
    > [!NOTE]  
    >  La especificación de un tipo de cuenta Individual es correcto para este escenario porque solo la aplicación de servicio PowerPivot solicitará las credenciales de la cuenta de actualización de datos desatendida de PowerPivot. En la práctica, la aplicación de servicio es el único usuario de la cuenta de actualización de datos desatendida, lo que hace que el tipo de cuenta Individual sea la mejor opción para esta aplicación de destino.  
  
8.  Omita la dirección URL de la página de la aplicación de destino. La actualización de datos PowerPivot no la utiliza.  
  
9. Haga clic en **Siguiente**.  
  
10. En la página **especificar los campos de credenciales para la aplicación de destino de almacenamiento seguro** , acepte los valores predeterminados. Los nombres de campo y los tipos deben ser Nombre de usuario Windows y Contraseña de Windows.  
  
11. Haga clic en **Siguiente**.  
  
12. En Administradores de la aplicación de destino, especifique la identidad del grupo de aplicaciones de la aplicación de servicio PowerPivot. El servicio requiere permisos de **control total** para que pueda recuperar información de la cuenta de actualización de datos desatendida en tiempo de ejecución. Además, especifique las cuentas de usuario de dominio de Windows de cualquier otro usuario de SharePoint que deba tener acceso administrativo a las opciones de configuración de la aplicación.  
  
13. Haga clic en **Aceptar**.  
  
14. Seleccione la aplicación de destino que acaba de crear, haga clic en la flecha abajo y seleccione **establecer credenciales.**  
  
15. En **propietarios de credenciales**, escriba una cuenta de usuario de dominio de Windows que desee que tenga permisos para actualizar las credenciales. Las credenciales se utilizan para las acciones de actualización de datos y los **propietarios de credenciales** tienen permisos para modificar las credenciales.  
  
16. Haga clic en **Aceptar**.  
  
###  <a name="step-2-specify-the-unattended-account-in-powerpivot-server-configuration-pages"></a><a name="bkmk_specifyUA"></a>Paso 2: especificar la cuenta desatendida en las páginas de configuración del servidor de PowerPivot  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Encuentre la aplicación de servicio PowerPivot. Puede identificar una aplicación de servicio por su tipo. Un tipo de aplicación de servicio PowerPivot es **Aplicación de servicio PowerPivot**.  
  
3.  Haga clic en el nombre de la aplicación de servicio PowerPivot. Espere a que aparezca el Panel de administración de PowerPivot.  
  
4.  En acciones, en la esquina superior derecha, haga clic en configurar las opciones de la **aplicación de servicio**.  
  
5.  En actualización de datos, en cuenta de actualización de datos desatendida de PowerPivot, escriba el identificador de la aplicación de destino que creó en un paso anterior: **PowerPivotDataRefresh**.  
  
6.  Haga clic en **Aceptar**.  
  
###  <a name="step-3-grant-contribute-permissions-to-the-account"></a><a name="bkmk_grant"></a>Paso 3: conceder permisos de contribución a la cuenta  
 Antes de poder usar la cuenta de actualización de datos desatendida de PowerPivot, se le deben asignar permisos de contribución en cualquier libro PowerPivot para el que se use. Este nivel de permisos es necesario para abrir el libro desde una biblioteca y, a continuación, volver a guardarlo en la biblioteca antes de que se actualicen los datos.  
  
 La asignación de permisos es un paso que lo realiza el administrador de la colección de sitios. Los permisos de SharePoint se pueden asignar en la colección de sitios raíz o en cualquier nivel inferior a este, incluidos documentos y elementos individuales. La forma en la que establezca los permisos variará en función de la pormenorización que necesite. En los siguientes pasos se muestra un enfoque para conceder permisos.  
  
1.  En un sitio de SharePoint, en acciones del sitio, haga clic en **permisos del sitio**.  
  
2.  Haga clic en **Concesión de permisos**.  
  
3.  En Seleccionar usuarios, escriba el nombre de la cuenta de usuario de dominio de Windows que designó como la cuenta desatendida de PowerPivot. Se trata del nombre de la cuenta de usuario de dominio de Windows que especificó en la aplicación de destino en el servicio de almacenamiento seguro.  
  
4.  En conceder permisos, seleccione **conceder permiso a los usuarios directamente**.  
  
5.  Seleccione **contribuir**y, a continuación, haga clic en **Aceptar**.  
  
###  <a name="step-4-grant-read-permissions-to-access-external-data-sources-used-in-data-refresh"></a><a name="bkmk_dbread"></a>Paso 4: conceder permisos de lectura para tener acceso a los orígenes de datos externos utilizados en la actualización de datos  
 Al importar datos a un libro PowerPivot, las conexiones con datos externos se suelen basar en conexiones de confianza o en conexiones suplantadas que utilizan la identidad del usuario actual para conectarse al origen de datos. Estos tipos de conexiones solo funcionan cuando el usuario actual tiene permiso para leer los datos que va a importar.  
  
 En un escenario de actualización de datos, la misma cadena de conexión que se usó para importar los datos se reutiliza ahora para actualizarlos. Si la cadena de conexión supone que el usuario es el actual (por ejemplo, una cadena que incluye Integrated_Security=SSPI), el Servicio de sistema de PowerPivot pasará la identidad del usuario de la cuenta de actualización de datos desatendida de PowerPivot como el usuario actual. Esta conexión solo tendrá éxito si la cuenta de actualización de datos desatendida de PowerPivot dispone de permisos de lectura en el origen de datos externo.  
  
 Por esta razón, debe conceder los permisos de solo lectura a la cuenta de actualización de datos desatendida de PowerPivot en todos los orígenes de datos externos que se usen en cualquier operación de actualización de datos que se ejecute en la cuenta desatendida.  
  
 Si es administrador de los orígenes de datos que se usan en su organización, puede crear un inicio de sesión y asignar los permisos necesarios. De lo contrario, debe ponerse en contacto con los propietarios de los datos y proporcionarles la información de las cuentas. Asegúrese de especificar la cuenta de usuario de dominio de Windows que se asigna a la cuenta de actualización de datos desatendida de PowerPivot. Esta es la cuenta que especificó en "(paso 1): crear una aplicación de destino y establecer las credenciales" en este tema.  
  
###  <a name="step-5-verify-account-availability-in-data-refresh-configuration-pages"></a><a name="bkmk_verify"></a>Paso 5: comprobar la disponibilidad de la cuenta en las páginas de configuración de actualización de datos  
  
1.  Abra una página de configuración de la actualización de datos para un libro publicado que contenga los datos PowerPivot. Para obtener instrucciones sobre cómo abrir la página, vea [programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
2.  Compruebe que la opción **usar la cuenta de actualización de datos configurada por el administrador** está habilitada en la página de configuración de actualización de datos.  
  
3.  Active la casilla **también actualizar lo más rápido posible** y, a continuación, haga clic en **Aceptar**.  
  
4.  En la biblioteca que contiene el libro, seleccione el libro, haga clic en la flecha abajo que aparece a la derecha y, a continuación, seleccione **administrar actualización de datos PowerPivot**. Es posible que tenga que esperar varios minutos si el trabajo de actualización de datos devuelve una gran cantidad de datos.  
  
 Si se produce un error, puede hacer clic en **Configurar programación** en la página historial de actualización de datos para probar otras credenciales. También puede que necesite inspeccionar la información de conexión de orígenes de datos en el libro original para ver la cadena de conexión que se utiliza durante la actualización de datos. La cadena de conexión proporcionará información sobre la ubicación del servidor y la base de datos que se pueden utilizar para solucionar el problema.  
  
 Para obtener más información acerca de la solución de problemas, consulte solución de problemas de la [actualización de datos PowerPivot](https://go.microsoft.com/fwlink/p/?LinkID=223279) en el sitio wiki de TechNet.  
  
##  <a name="using-the-powerpivot-unattended-data-refresh-account"></a><a name="bkmk_use"></a>Usar la cuenta de actualización de datos desatendida de PowerPivot  
 De las tres opciones de credencial de la página de programación de actualización de datos PowerPivot, solo la primera corresponde a la cuenta de actualización de datos desatendida. Asegúrese de seleccionar esta opción al preparar la programación de la actualización de datos.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 No utilice la tercera opción de credencial (la que exige que escriba el identificador de la aplicación de destino) para acceder a la cuenta de actualización de datos desatendida de PowerPivot. Existe una comprobación de suplantación adicional que se realiza con esta opción que producirá un error de validación si intenta utilizarlo con la cuenta de actualización de datos desatendida de PowerPivot (o cualquier aplicación de destino que se base en el tipo de cuenta Individual). Para obtener más información sobre cómo usar la tercera opción, vea [configurar credenciales almacenadas para la actualización de datos PowerPivot &#40;PowerPivot para SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
##  <a name="update-the-credentials-used-by-an-existing-powerpivot-unattended-data-refresh-account"></a><a name="bkmk_editUA"></a>Actualizar las credenciales utilizadas por una cuenta de actualización de datos desatendida de PowerPivot existente  
 Si la cuenta de actualización de datos desatendida ya se ha configurado en la instalación o la ha configurado un administrador, puede actualizar el nombre de usuario o la contraseña modificando la aplicación de destino que almacene las credenciales. Tenga en cuenta que la identidad de Windows original que se asoció previamente con cuenta de actualización de datos desatendida de PowerPivot no estará visible cuando modifique las credenciales en Servicio de almacenamiento seguro. Si está actualizando una contraseña caducada o especificando una cuenta diferente, tiene que volver a escribir siempre el nombre de usuario y la contraseña para esa aplicación de destino en Servicio de almacenamiento seguro.  
  
1.  En Administración central, en Administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en **servicio de almacenamiento seguro**.  
  
3.  Active la casilla situada junto a **PowerPivotDataRefresh**.  
  
4.  En credenciales, haga clic en **establecer**.  
  
5.  En **propietarios de credenciales**, escriba una cuenta de usuario de dominio de Windows que desee que tenga permisos para actualizar las credenciales. Las credenciales se utilizan para las acciones de actualización de datos y los **propietarios de credenciales** tienen permisos para modificar las credenciales.  
  
6.  En Nombre de usuario, escriba la cuenta de usuario de dominio de Windows que formará parte de las credenciales de la actualización de datos desatendida.  
  
7.  En Contraseña, escriba la contraseña de la cuenta y, a continuación, vuelva a escribirla para confirmarla.  
  
8.  Haga clic en **Aceptar**.  
  
 Si desea cambiar no solo la contraseña, sino también el nombre de usuario de la cuenta, probablemente tendrá que realizar pasos de configuración adicionales, como conceder permisos de lectura a orígenes de datos externos y permisos de SharePoint para actualizar el libro PowerPivot. Para obtener instrucciones, vaya a este paso en configuración de la cuenta de actualización de datos desatendida de PowerPivot: [paso 3: conceda permisos de contribución a la cuenta](#bkmk_grant)y, a continuación, continúe con todos los pasos restantes, y concluya con la comprobación de que la cuenta está configurada correctamente.  
  
## <a name="see-also"></a>Consulte también  
 [Actualización de datos PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)   
 [Programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Actualización de datos PowerPivot](power-pivot-sharepoint/power-pivot-data-refresh.md)  
  
  
