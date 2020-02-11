---
title: Configurar credenciales almacenadas para la actualización de datos PowerPivot (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 987eff0f-bcfe-4bbd-81e0-9aca993a2a75
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23f35c8998b204182f25f85f8f7694fb60d042b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087460"
---
# <a name="configure-stored-credentials-for-powerpivot-data-refresh-powerpivot-for-sharepoint"></a>Configurar las credenciales almacenadas para la actualización de datos PowerPivot (PowerPivot para SharePoint)
  Los trabajos de actualización de datos PowerPivot se pueden ejecutar en cualquier cuenta de usuario de Windows, siempre que cree una aplicación de destino en el Servicio de almacenamiento seguro para almacenar las credenciales que desea utilizar. De igual forma, si desea proporcionar un inicio de sesión de base de datos que no sea el utilizado originalmente para importar los datos en PowerPivot para Excel, puede asignar esas credenciales a una aplicación de destino del Servicio de almacenamiento seguro y, a continuación, especificar esa aplicación de destino en una programación de actualización de datos.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
 Después de seguir las instrucciones incluidas en este tema, podrá utilizar la siguiente opción de credenciales en la página de programación de actualización de datos PowerPivot:  
  
 ![SSAS_PowerPivotDataRefreshCreds_Stored](media/ssas-powerpivotdatarefreshcreds-stored.gif "SSAS_PowerPivotDataRefreshCreds_Stored")  
  
 En este tema se explica cómo configurar los nombres de usuario y las contraseñas que se utilizan para la actualización de datos PowerPivot en una granja de SharePoint 2010. Antes de realizar estos pasos, debe de haber habilitado el Servicio de almacenamiento seguro y haber generado una clave maestra. Para obtener más información, vea [actualización de datos PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
 Este tema contiene las siguientes secciones:  
  
 [Configurar una cuenta de Windows para la actualización de datos](#configAny)  
  
 [Configurar una cuenta predefinida para tener acceso a orígenes de datos externos o de otros proveedores](#config3rd)  
  
 Si tiene problemas para configurar o usar la actualización de datos, consulte la página de solución de problemas de la [actualización de datos PowerPivot](https://go.microsoft.com/fwlink/?LinkID=223279) en el sitio wiki de TechNet para ver posibles soluciones.  
  
##  <a name="configAny"></a>Configurar cualquier cuenta de Windows para la actualización de datos  
 Cuando un usuario de SharePoint define una programación de actualización de datos, debe especificar la identidad del usuario bajo la que se realiza la actualización de datos. Para hacerlo, puede seleccionar la cuenta de actualización de datos desatendida de PowerPivot, escribir su cuenta de usuario de dominio de Windows, o escribir otra cuenta de usuario de Windows que sea válida con fines de actualización de datos. Los pasos descritos en esta sección son para realizar la última opción: especificar otra cuenta de Windows.  
  
 Puede elegir este método si desea una alternativa al uso de la cuenta de actualización de datos desatendida de PowerPivot (disponible para todos los usuarios de PowerPivot en SharePoint) o de las credenciales del propietario del libro. Por ejemplo, podría interesarle poner varias cuentas de actualización de datos a disposición de distintos grupos de trabajo, de forma que le sea más fácil realizar el seguimiento y administrar la actividad de actualización de datos en el nivel de la organización.  
  
> [!IMPORTANT]  
>  Las personas y aplicaciones que utilizan esta aplicación de destino (y las credenciales que almacena) deben aparecer como miembros de la aplicación. Debe agregar la identidad de cada aplicación de servicio PowerPivot que utilizará la aplicación de destino, su cuenta de Windows y las cuentas de usuario o de grupo de las personas que vayan a especificar esta aplicación de destino en sus programaciones de actualización de datos. Puede especificar todas estas cuentas al crear la aplicación de destino. Si no sabe todas las cuentas de usuario y de grupo que requerirán acceso a esta aplicación, puede agregarlas posteriormente una vez creada la aplicación de destino.  
  
 Hay 4 pasos para configurar credenciales almacenadas para la actualización de datos:  
  
-   Cree la aplicación de destino que almacena las credenciales.  
  
-   Conceda permisos de contribución a la cuenta.  
  
-   Conceda permisos de lectura a la cuenta para tener acceso a los orígenes de datos externos durante la actualización de datos.  
  
-   Compruebe que la actualización de datos funciona al especificar esta aplicación de destino en una programación de actualización de datos.  
  
### <a name="step-1-create-a-target-application"></a>Paso 1: crear un identificador de la aplicación de destino  
  
1.  En administración central, en administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en **servicio de almacenamiento seguro**.  
  
3.  En administrar aplicaciones de destino, haga clic en **nuevo**.  
  
4.  Como identificador de la aplicación de destino, escriba una cadena de texto. La cadena debe ser única, pero también debería ser fácil de recordar. Los usuarios escribirán esta cadena en las páginas de la programación de actualización de datos cada vez que deseen utilizar las credenciales que están almacenadas en esta aplicación.  
  
5.  En Nombre para mostrar, escriba un nombre descriptivo. Este nombre solo se utiliza para la presentación. No se usa para especificar la aplicación de destino en una programación de actualización de datos.  
  
6.  En Correo electrónico de contacto, escriba su dirección de correo electrónico.  
  
7.  En tipo de aplicación de destino, seleccione **Grupo**.  
  
    > [!IMPORTANT]  
    >  Es necesario elegir el tipo de cuenta Grupo, porque permite especificar todas las cuentas de servicio y usuario solicitando acceso a las credenciales. Para cada solicitud, el Servicio de sistema de PowerPivot comprueba si el solicitante es un miembro de la aplicación de destino.  
  
8.  Omita la dirección URL de la página de la aplicación de destino. La actualización de datos PowerPivot no la utiliza.  
  
9. Haga clic en **Next**.  
  
10. En la página **especificar los campos de credenciales para la aplicación de destino de almacenamiento seguro** , acepte los valores predeterminados. Los nombres de campo y los tipos deben ser el nombre de usuario de Windows y la contraseña de Windows.  
  
11. Haga clic en Siguiente.  
  
12. En Administradores de la aplicación de destino, especifique las cuentas de usuario de dominio de Windows de los usuarios de SharePoint que deberían tener acceso administrativo a las configuraciones de la aplicación de destino (por ejemplo, la capacidad de agregar o quitar cuentas en la lista Miembros).  
  
13. En Miembros, agregue las siguientes cuentas de usuario y de grupo:  
  
    1.  Dado que crea la aplicación, agregue su cuenta de usuario de Windows a la lista Miembros.  
  
    2.  Agregue la identidad del grupo de aplicaciones de la aplicación de servicio PowerPivot para que pueda recuperar las credenciales cuando la actualización de datos se programe para ejecutarse. Para ver la identidad del grupo de aplicaciones, vaya a **Administrar aplicaciones de servicio**, seleccione la aplicación de servicio PowerPivot haciendo clic en el espacio vacío situado junto al nombre (Esto selecciona la fila) y, a continuación, haga clic en **propiedades**. La cuenta de seguridad que aparece en esta página es la cuenta que desea agregar como miembro de la aplicación de destino.  
  
    3.  Agregue cuentas de usuario y grupo de Windows que vayan a tener acceso a esta aplicación de destino en las programaciones de la actualización de datos.  
  
14. Haga clic en **OK**.  
  
15. Seleccione la aplicación de destino que acaba de crear, haga clic en la flecha abajo y seleccione **establecer credenciales.**  
  
16. En Propietario de la Credencial, observe que la lista de propietarios de credenciales es de solo lectura. Las cuentas que tienen propiedad sobre las credenciales son los miembros de la aplicación de destino. Para agregar o quitar un propietario de credencial, debe agregar o quitar cuentas en la lista de miembros de la aplicación de destino.  
  
     En Nombre de usuario de Windows y Contraseña de Windows, escriba las credenciales de la cuenta de usuario de Windows que se utilizará para ejecutar la actualización de datos.  
  
17. Haga clic en **OK**.  
  
###  <a name="bkmk_grant"></a>Paso 2: conceder permisos de contribución a la cuenta  
 Para poder utilizar las credenciales almacenadas, la cuenta debe tener asignados permisos de contribución en cualquier libro PowerPivot para el que se use. Este nivel de permisos es necesario para abrir el libro desde una biblioteca y, a continuación, volver a guardarlo en la biblioteca antes de que se actualicen los datos.  
  
 La asignación de permisos es un paso que lo realiza el administrador de la colección de sitios. Los permisos de SharePoint se pueden asignar en la colección de sitios raíz o en cualquier nivel inferior a este, incluidos documentos y elementos individuales. La forma en la que establezca los permisos variará en función de la pormenorización que necesite. En los siguientes pasos se muestra un enfoque para conceder permisos.  
  
1.  En un sitio de SharePoint, en acciones del sitio, haga clic en **permisos del sitio**.  
  
2.  Haga clic en **Concesión de permisos**.  
  
3.  En Seleccionar usuarios, escriba el nombre de la cuenta de usuario de dominio de Windows que especificó en la aplicación de destino.  
  
4.  En conceder permisos, seleccione **conceder permiso a los usuarios directamente**.  
  
5.  Seleccione **contribuir**y, a continuación, haga clic en **Aceptar**.  
  
###  <a name="bkmk_dbread"></a>Paso 3: conceder permisos de lectura para tener acceso a los orígenes de datos externos utilizados en la actualización de datos  
 Al importar datos a un libro PowerPivot, las conexiones con datos externos se suelen basar en conexiones de confianza o en conexiones suplantadas que utilizan la identidad del usuario actual para conectarse al origen de datos. Estos tipos de conexiones solo funcionan cuando el usuario actual tiene permiso para leer los datos que va a importar.  
  
 En un escenario de actualización de datos, la misma cadena de conexión que se usó para importar los datos se reutiliza ahora para actualizarlos. Si la cadena de conexión supone que el usuario es el actual (por ejemplo, una cadena que incluye Integrated_Security=SSPI), el Servicio de sistema de PowerPivot pasará la identidad del usuario especificado en la aplicación de destino como usuario actual. Esta conexión solo tendrá éxito si la cuenta dispone de permisos de lectura en el origen de datos externo.  
  
 Por esta razón, debe conceder los permisos de solo lectura a la cuenta en todos los orígenes de datos externos que se utilicen durante la actualización de datos.  
  
 Si es administrador de los orígenes de datos que se usan en su organización, puede crear un inicio de sesión y asignar los permisos necesarios. De lo contrario, debe ponerse en contacto con los propietarios de los datos y proporcionarles la información de las cuentas. Asegúrese de especificar la cuenta de usuario de dominio de Windows que se asigne a la aplicación de destino. Esta es la cuenta que especificó en "paso 1: crear una aplicación de destino" en este tema.  
  
###  <a name="bkmk_verify"></a>Paso 4: comprobar la disponibilidad de la cuenta en las páginas de configuración de actualización de datos  
  
1.  Abra una página de configuración de la actualización de datos para un libro publicado que contenga los datos PowerPivot. Para obtener instrucciones sobre cómo abrir la página, vea [programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
2.  Compruebe que la opción **conectar con las credenciales guardadas en servicio de almacenamiento seguro (SSS) para iniciar sesión en el origen de datos** está habilitada en la página de configuración de la actualización de datos y, a continuación, escriba el nombre de la aplicación de destino.  
  
3.  Active la casilla **también actualizar lo más rápido posible** y, a continuación, haga clic en **Aceptar**.  
  
4.  En la biblioteca que contiene el libro, seleccione el libro, haga clic en la flecha abajo que aparece a la derecha y, a continuación, seleccione **administrar actualización de datos PowerPivot**. Es posible que tenga que esperar varios minutos si el trabajo de actualización de datos devuelve una gran cantidad de datos.  
  
 Si se produce un error, puede hacer clic en **Configurar programación** en la página historial de actualización de datos para probar otras credenciales. También puede que necesite inspeccionar la información de conexión de orígenes de datos en el libro original para ver la cadena de conexión que se utiliza durante la actualización de datos. La cadena de conexión proporcionará información sobre la ubicación del servidor y la base de datos que se pueden utilizar para solucionar el problema.  
  
 Para obtener más información acerca de la solución de problemas, consulte solución de problemas de la [actualización de datos PowerPivot](https://go.microsoft.com/fwlink/p/?LinkID=223279) en el sitio wiki de TechNet.  
  
##  <a name="config3rd"></a>Configurar una cuenta predefinida para tener acceso a orígenes de datos externos o de terceros  
 Los servidores de la base de datos a menudo vienen con sus propios métodos de autenticación. Si tiene un libro PowerPivot que requiere que las credenciales de la base de datos tengan acceso a un origen de datos externo durante la actualización de datos, puede crear un identificador de la aplicación de destino para las credenciales y, a continuación, especificar la aplicación de destino en la sección Orígenes de datos de la página de actualización de datos de programación.  
  
 Este paso solo es necesario si desea proporcionar a los usuarios una opción para invalidar las credenciales de la base de datos que ya estén incrustadas en el libro PowerPivot.  
  
 Este paso solo funciona si la cadena de conexión ya incluye un nombre de usuario y una contraseña. Tenga en cuenta que tener credenciales en la cadena de conexión es relativamente raro, de modo que su capacidad para utilizar esta opción será, en cierto modo, limitada. En la mayoría de los casos, tendrá solo un identificador de usuario y una contraseña en la cadena de conexión si utiliza la autenticación de la base de datos para conectarse al origen de datos. Para obtener más información acerca de cómo comprobar la cadena de conexión para ver si incluye un identificador de usuario y una contraseña, vea la sección "conceder permisos para crear programaciones y obtener acceso a datos externos" en la [actualización de datos PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md).  
  
1.  En administración central, en administración de aplicaciones, haga clic en **Administrar aplicaciones de servicio**.  
  
2.  Haga clic en **servicio de almacenamiento seguro**.  
  
3.  En administrar aplicaciones de destino, haga clic en **nuevo**.  
  
4.  Como identificador de la aplicación de destino, escriba una cadena de texto. La cadena debe ser única, pero también debería ser fácil de recordar. Los usuarios escribirán esta cadena en las páginas de la programación de actualización de datos cada vez que deseen utilizar las credenciales que están almacenadas en esta aplicación.  
  
5.  En Nombre para mostrar, escriba un nombre descriptivo. Este nombre solo se utiliza para la presentación. No se usa para especificar la aplicación de destino en una programación de actualización de datos.  
  
6.  En Correo electrónico de contacto, escriba su dirección de correo electrónico.  
  
7.  En tipo de aplicación de destino, seleccione **Grupo**.  
  
8.  Omita la dirección URL de la página de la aplicación de destino. La actualización de datos PowerPivot no la utiliza.  
  
9. Haga clic en **Next**.  
  
10. En la página **especificar los campos de credenciales para la aplicación de destino de almacenamiento seguro** , acepte los valores predeterminados solo si el origen de datos usa la autenticación de Windows. En caso contrario, elija los tipos de campo que sean válidos para el origen de datos y, a continuación, modifique los nombres de campo de forma que coincidan con el tipo.  
  
     Por ejemplo, podría especificar Nombre de usuario de SQL Server y Contraseña de usuario de SQL Server como los nombres de campo y, a continuación, elegir Nombre de usuario y Contraseña para los tipos de campo.  
  
11. Haga clic en Siguiente.  
  
12. En Administradores de la aplicación de destino, especifique las cuentas de usuario de dominio de Windows de los usuarios de SharePoint que deberían tener acceso administrativo a las configuraciones de la aplicación.  
  
13. En Miembros, agregue las siguientes cuentas de usuario y de grupo:  
  
    1.  Dado que crea la aplicación, agregue su cuenta de usuario de Windows a la lista Miembros.  
  
    2.  Agregue la identidad del grupo de aplicaciones de cada aplicación de servicio PowerPivot que vaya a utilizar la aplicación de destino para tener acceso a sus credenciales almacenadas. Para ver la identidad, vaya a **Administrar aplicaciones de servicio**, seleccione la aplicación de servicio PowerPivot haciendo clic en el espacio vacío situado junto al nombre (Esto selecciona la fila) y, a continuación, haga clic en **propiedades**. La cuenta de seguridad que aparece en esta página es la cuenta que desea agregar como un miembro de la aplicación de destino.  
  
    3.  Agregue las cuentas de usuario y grupo de Windows que vayan a tener acceso a esta aplicación de destino en la sección de orígenes de datos de una página de programación de actualización de datos.  
  
14. Haga clic en **OK**.  
  
15. Seleccione la aplicación de destino que acaba de crear, haga clic en la flecha abajo y seleccione **establecer credenciales.**  
  
16. Escriba las credenciales que se utilizarán para conectarse al origen de datos (por ejemplo, el nombre de usuario y la contraseña de un inicio de sesión de SQL Server).  
  
17. Haga clic en **OK**.  
  
## <a name="see-also"></a>Consulte también  
 [Programar una actualización de datos &#40;PowerPivot para SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Actualización de datos PowerPivot con SharePoint 2010](powerpivot-data-refresh-with-sharepoint-2010.md)  
  
  
