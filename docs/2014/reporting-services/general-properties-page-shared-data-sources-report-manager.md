---
title: Página Propiedades generales, comparten los orígenes de datos (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 1b344449-6f7c-47d2-a737-972d88c0faf8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a50b1b947ce82eb38ef7c7f6fd026bc9f83376f4
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59964888"
---
# <a name="general-properties-page-shared-data-sources-report-manager"></a>Página Propiedades generales, Orígenes de datos compartidos (Administrador de informes)
  Use la página de propiedades General para ver o modificar las propiedades de un elemento de origen de datos compartido. Al hacer clic en **Aplicar**, los cambios efectuados en las propiedades afectan a todos los informes que hagan referencia al elemento.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
###### <a name="to-open-the-general-properties-page-for-a-shared-data-source"></a>Para abrir la página de propiedades General de un origen de datos compartido  
  
1.  Abra el Administrador de informes y busque el origen de datos compartido del que desea ver las propiedades.  
  
2.  Mantenga el mouse sobre el origen de datos y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Esto abre la página de propiedades General del origen de datos compartido.  
  
## <a name="options"></a>Opciones  
 **Name**  
 Especifica un nombre para el origen de datos compartido, que se utiliza para identificar el elemento en el espacio de nombres del servidor de informes.  
  
 **Descripción**  
 Proporciona información sobre el origen de datos compartido. Esta descripción aparecerá en la página Contenido.  
  
 **Ocultar en la vista de lista**  
 Seleccione esta opción para ocultar el origen de datos compartido a usuarios que usen el modo de vista de lista en el Administrador de informes. El modo de vista de lista es el formato de vista predeterminado al explorar la jerarquía de carpetas del servidor de informes. En la vista de lista, los nombres y descripciones de elementos se presentan en formato horizontal. El formato alternativo es la vista Detalles. La vista Detalles no incluye descripciones, pero sí otra información acerca del elemento. Aunque se puede ocultar un elemento en la vista de lista, no se puede ocultar en la vista Detalles. Si desea restringir el acceso a un elemento, deberá crear una asignación de roles.  
  
 **Habilitar este origen de datos**  
 Seleccione esta opción para habilitar o deshabilitar el origen de datos compartido. Puede deshabilitar el origen de datos compartido para impedir que se procesen todos los informes, modelos de informe y suscripciones controladas por datos que hagan referencia al elemento.  
  
 **Tipo de origen de datos**  
 Especifica la extensión de procesamiento de datos que se va a utilizar para procesar los datos del origen de datos. El servidor de informes incluye extensiones de procesamiento de datos para [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], Oracle, XML, SAP, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], ODBC y OLE DB. Es posible que otros fabricantes ofrezcan extensiones de procesamiento de datos adicionales.  
  
 Tenga en cuenta que si está usando [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] Edition con Advanced Services, solo puede elegir orígenes de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Cadena de conexión**  
 Especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. El tipo de conexión determina la sintaxis que debería usar. Por ejemplo, una cadena de conexión para la extensión de procesamiento de datos XML es una dirección URL a un documento XML. En la mayoría de los casos, la cadena de conexión típica especifica el servidor de bases de datos y un archivo de datos. En el ejemplo siguiente, se muestra la cadena de conexión que se usa para establecer conexión con la base de datos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBnormal](../includes/sssampledbnormal-md.md)] :  
  
```  
data source=<a SQL Server instance>;initial catalog=AdventureWorks2012  
```  
  
 **Conectar utilizando**  
 Especifica las opciones que determinan cómo se obtienen las credenciales.  
  
> [!IMPORTANT]  
>  Si las credenciales se suministran en la cadena de conexión, se omiten las opciones y los valores que se proporcionan en esta sección. Tenga en cuenta que, si especifica las credenciales en la cadena de conexión, todos los usuarios que abran esta página verán los valores como texto no cifrado.  
  
 **Credenciales suministradas por el usuario que ejecuta el informe**  
 Cada usuario debe escribir un nombre de usuario y una contraseña para acceder al origen de datos. Puede definir el texto del mensaje que solicita las credenciales del usuario. La cadena de texto predeterminada es "Especifique un nombre de usuario y una contraseña para tener acceso al origen de datos".  
  
 Seleccione **Usar como credenciales de Windows para la conexión al origen de datos** si las credenciales que el usuario suministra son las credenciales de autenticación de Windows. No la active si va a utilizar la autenticación de la base de datos (por ejemplo, la autenticación de SQL Server).  
  
 **Credenciales almacenadas de forma segura en el servidor de informes**  
 Almacene un nombre de usuario y una contraseña cifrados en la base de datos del servidor de informes. Seleccione esta opción para ejecutar un informe de manera desatendida; por ejemplo, informes iniciados por programaciones o eventos en lugar de una acción del usuario. Si va a usar la seguridad predeterminada, el nombre de usuario debe ser una cuenta de dominio de Windows. Especifique la cuenta con este formato: \<dominio >\\< nombre de usuario\>. La cuenta que especifica debe tener permisos de inicio de sesión local en el equipo que hospeda el origen de datos usado por el informe.  
  
 Active la casilla **Utilizar como credenciales de Windows para la conexión al origen de datos** si las credenciales son las credenciales de autenticación de Windows. No active esta casilla si va a usar la autenticación de la base de datos (por ejemplo, autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ).  
  
 Si está usando autenticación de la base de datos, seleccione **Suplantar al usuario autenticado después de realizar una conexión al origen de datos (Conectar utilizando)** para permitir la delegación de credenciales de la base de datos pero solo si un servidor de bases de datos admite la suplantación. En el caso de las bases de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , esta opción establece la función SETUSER.  
  
 **Seguridad integrada de Windows**  
 Use las credenciales de Windows del usuario actual para obtener acceso al origen de datos. Seleccione esta opción cuando las credenciales que se usan para obtener acceso a un origen de datos son las mismas que se usaron para iniciar sesión en el dominio de red. Esta opción funciona de manera óptima cuando Kerberos está habilitado para el dominio o cuando el origen de datos se encuentra en el mismo equipo que el servidor de informes. Si Kerberos no está habilitado, se pueden pasar las credenciales de Windows a otro equipo. Si se requieren más conexiones de equipos, obtendrá un error en lugar de los datos esperados.  
  
 Un administrador del servidor de informes puede deshabilitar el uso de seguridad integrada de Windows para tener acceso a los orígenes de datos del informe. Si este valor está deshabilitado, la característica no está disponible.  
  
 No use esta opción si piensa programar o suscribirse a este informe. El procesamiento de informes desatendido o programado requiere credenciales que se pueden obtener sin datos proporcionados por el usuario o el contexto de seguridad de un usuario actual. Solo las credenciales almacenadas proporcionan esta capacidad. Por este motivo, el servidor de informes evita que programe el procesamiento de informes o suscripciones si el informe está configurado para el tipo de credencial de seguridad integrada de Windows. Si elige esta opción para un informe al que ya está suscrito o que tiene operaciones programadas, se detendrán las suscripciones y las operaciones programadas.  
  
 **No se necesitan credenciales**  
 Especifique que no se necesitan credenciales para obtener acceso al origen de datos. Tenga en cuenta que, si un origen de datos requiere un inicio de sesión de usuario, esta opción no tendrá ningún efecto. Elija esta opción solo si la conexión al origen de datos no requiere credenciales de usuario.  
  
 Para usar esta opción, debe haber configurado previamente la cuenta de ejecución desatendida para la implementación del servidor de informes. La cuenta de ejecución desatendida se usa para conectarse a los orígenes de datos externos cuando otros orígenes de credenciales no están disponibles. Si especifica esta opción y la cuenta no está configurada, se producirá un error en la conexión al origen de datos del informe y no se producirá el procesamiento de informes. Para obtener más información acerca de esta cuenta, consulte [configurar la cuenta de ejecución desatendida &#40;SSRS Configuration Manager&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 **Aplicar**  
 Haga clic para guardar los cambios.  
  
 **Eliminar**  
 Haga clic para eliminar el origen de datos compartido. Si elimina un origen de datos compartido, se deshabilitarán todos los informes, modelos y suscripciones controladas por datos que lo utilicen. Para volver a activar los informes, modelos y suscripciones, deberá abrirlos uno a uno y actualizar sus propiedades de origen de datos de modo que utilicen un origen de datos compartido distinto. En el caso de informes y suscripciones, puede especificar información de conexión de origen de datos como valores de propiedad de origen de datos.  
  
 **Mover**  
 Haga clic para mover el origen de datos compartido a otra ubicación del espacio de nombres de carpetas del servidor de informes.  
  
 **Generar modelo**  
 Haga clic para crear un nuevo modelo basado en el origen de datos compartido.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de informes &#40;Modo nativo de SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Nuevo origen de datos &#40;página del Administrador de informes&#41;](../../2014/reporting-services/new-data-source-page-report-manager.md)   
 [El Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)   
 [Especificación de información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)  
  
  
