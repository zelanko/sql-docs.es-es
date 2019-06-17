---
title: Origen de datos nueva página (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 35563d4c-a3d5-4f95-bf46-605da9dfcbb8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 9cc4dda934496bbfa33306537b515870f0de23de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108175"
---
# <a name="new-data-source-page-report-manager"></a>Nuevo origen de datos (página del Administrador de informes)
  Use la página Nuevo origen de datos para crear un elemento de origen de datos compartido. Un origen de datos compartido define una conexión a un origen de datos externo. Con un origen de datos compartido, se puede crear y mantener la configuración de la conexión al origen de datos independientemente de los informes, modelos y suscripciones controladas por datos que usan el origen de datos.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-new-data-source-page"></a>Para abrir la página Nuevo origen de datos  
  
1.  Abra el Administrador de informes y desplácese hasta la carpeta en la que desea crear un origen de datos.  
  
2.  En la barra de herramientas, haga clic en **Nuevo origen de datos**. Debe tener los permisos de Administrador de contenido para crear un origen de datos compartido.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Escriba un nombre para el origen de datos compartido, que se usa para identificar el elemento en la jerarquía de carpetas del servidor de informes.  
  
 **Descripción**  
 Proporcione información sobre el origen de datos compartido. Esta descripción aparecerá en la página Contenido.  
  
 **Ocultar en la vista de lista**  
 Seleccione esta opción para ocultar el origen de datos compartido a usuarios que usen el modo de vista de lista en el Administrador de informes. El modo de vista de lista es el formato de vista predeterminado al explorar la jerarquía de carpetas del servidor de informes. En la vista de lista, los nombres y descripciones de elementos se presentan en formato horizontal. El formato alternativo es la vista Detalles. La vista Detalles no incluye descripciones, pero sí otra información acerca del elemento. Aunque se puede ocultar un elemento en la vista de lista, no se puede ocultar en la vista Detalles. Si desea restringir el acceso a un elemento, deberá crear una asignación de roles.  
  
 **Habilitar este origen de datos**  
 Seleccione esta opción para habilitar o deshabilitar el origen de datos compartido. Puede deshabilitar el origen de datos compartido para impedir que se procesen todos los informes y modelos que hagan referencia al elemento.  
  
 **Tipo de origen de datos**  
 Especifique la extensión de procesamiento de datos que se va a utilizar para procesar los datos del origen de datos. El servidor de informes incluye extensiones de procesamiento de datos para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], SAP, XML, ODBC y OLE DB. Es posible que otros fabricantes ofrezcan extensiones de procesamiento de datos adicionales.  
  
 Para obtener más información sobre la compatibilidad de origen de datos remotos y ajenos a SQL, consulte [características compatibles con las ediciones de SQL Server 2012](https://go.microsoft.com/fwlink/?linkid=232473) (HYPERLINK "<https://go.microsoft.com/fwlink/?linkid=232473>" <https://go.microsoft.com/fwlink/?linkid=232473>) y [Data Sources Supported by Reporting Servicios &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md).  
  
 **Cadena de conexión**  
 Especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. El tipo de conexión determina la sintaxis que debería usar. Por ejemplo, una cadena de conexión para la extensión de procesamiento de datos XML es una dirección URL a un documento XML. En la mayoría de los casos, la cadena de conexión típica especifica el servidor de bases de datos y un archivo de datos.  
  
 En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer conexión con la base de datos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] :  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 Para obtener más información y ejemplos acerca de diferentes maneras de especificar una cadena de conexión, consulte [conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
 **Conectar utilizando**  
 Especifique las opciones que determinan cómo se obtienen las credenciales.  
  
> [!IMPORTANT]  
>  Si las credenciales se suministran en la cadena de conexión, se omiten las opciones y los valores que se proporcionan en esta sección. Tenga en cuenta que, si especifica las credenciales en la cadena de conexión, todos los usuarios que abran esta página verán los valores como texto no cifrado.  
  
 **Credenciales suministradas por el usuario que ejecuta el informe (Conectar usando)**  
 Cada usuario debe escribir un nombre de usuario y una contraseña para obtener acceso al origen de datos. Puede definir el texto del mensaje que solicita las credenciales del usuario. La cadena de texto predeterminada es "Especifique un nombre de usuario y una contraseña para tener acceso al origen de datos".  
  
 Seleccione **Usar como credenciales de Windows para la conexión al origen de datos** si las credenciales que el usuario suministra son las credenciales de autenticación de Windows. No active esta casilla si va a usar la autenticación de la base de datos (por ejemplo, autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ).  
  
 **Credenciales almacenadas de forma segura en el servidor de informes (Conectar usando)**  
 Almacene un nombre de usuario y una contraseña cifrados en la base de datos del servidor de informes. Elija esta opción para ejecutar un informe de manera desatendida; por ejemplo, informes iniciados por programaciones o eventos en lugar de una acción del usuario. Si va a usar la seguridad predeterminada, el nombre de usuario debe ser una cuenta de dominio de Windows. Especifique la cuenta con este formato: \<dominio >\\< nombre de usuario\>. La cuenta que especifica debe tener permisos de inicio de sesión local en el equipo que hospeda el origen de datos usado por el informe.  
  
 Active la casilla **Utilizar como credenciales de Windows para la conexión al origen de datos** si las credenciales son las credenciales de autenticación de Windows. No active esta casilla si va a usar la autenticación de la base de datos (por ejemplo, autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ).  
  
 Si está usando la autenticación de base de datos, seleccione **Suplantar al usuario autenticado después de realizar una conexión al origen de datos** para permitir la delegación de las credenciales de la base de datos, pero solo si un servidor de base de datos admite la suplantación. En el caso de las bases de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , esta opción establece la función SETUSER.  
  
 **Seguridad integrada de Windows (Conectar usando)**  
 Use las credenciales de Windows del usuario actual para obtener acceso al origen de datos. Elija esta opción cuando las credenciales que se utilizan para obtener acceso a un origen de datos son las mismas que se utilizaron para iniciar sesión en el dominio de red. Esta opción funciona de manera óptima cuando la autenticación Kerberos está habilitada para el dominio o cuando el origen de datos se encuentra en el mismo equipo que el servidor de informes. Si la autenticación de Kerberos no está habilitada, se pueden pasar las credenciales de Windows a otro equipo. Si se requieren más conexiones de equipos, obtendrá un error en lugar de los datos esperados.  
  
 Un administrador del servidor de informes puede deshabilitar el uso de seguridad integrada de Windows para tener acceso a los orígenes de datos del informe. Si este valor está deshabilitado, la característica no está disponible.  
  
 No use esta opción si piensa programar o suscribirse a este informe. El procesamiento de informes desatendido o programado requiere credenciales que se pueden obtener sin datos proporcionados por el usuario o el contexto de seguridad de un usuario actual. Solo las credenciales almacenadas proporcionan esta capacidad. Por este motivo, el servidor de informes evita que programe el procesamiento de informes o suscripciones si el informe está configurado para el tipo de credencial de seguridad integrada de Windows. Si elige esta opción para un informe al que ya está suscrito o que tiene operaciones programadas, se detendrán las suscripciones y las operaciones programadas.  
  
 **No se necesitan credenciales (Conectar usando)**  
 Especifique que no se necesitan credenciales para obtener acceso al origen de datos. Tenga en cuenta que, si un origen de datos requiere un inicio de sesión de usuario, esta opción no tendrá ningún efecto. Elija esta opción solo si la conexión al origen de datos no requiere credenciales de usuario.  
  
 Para usar esta opción, debe haber configurado previamente la cuenta de ejecución desatendida para la implementación del servidor de informes. La cuenta de ejecución desatendida se usa para conectarse a los orígenes de datos externos cuando otros orígenes de credenciales no están disponibles. Si especifica esta opción y la cuenta no está configurada, se producirá un error en la conexión al origen de datos del informe y no se producirá el procesamiento de informes. Para obtener más información acerca de esta cuenta, consulte [configurar la cuenta de ejecución desatendida &#40;SSRS Configuration Manager&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 **Aceptar**  
 Haga clic para guardar los cambios.  
  
## <a name="see-also"></a>Vea también  
 [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Contenido &#40;página del Administrador de informes&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Crear, modificar y eliminar orígenes de datos compartidos &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [El Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)   
 [Especificación de información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
