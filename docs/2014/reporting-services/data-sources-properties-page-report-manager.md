---
title: Orígenes de datos de la página de propiedades (Administrador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f37edda0-19e6-489e-b544-8751fa6b6cfb
caps.latest.revision: 35
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: e826f27b2ce6bbb75d4aabc9d8537d0f867a0cce
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179562"
---
# <a name="data-sources-properties-page-report-manager"></a>Orígenes de datos (página de propiedades del Administrador de informes)
  Use la página de propiedades Orígenes de datos para definir la manera en que el informe actual se conecta a un origen de datos externo. Puede reemplazar la información de conexión con el origen de datos originalmente publicada con el informe. Si se utilizan varios orígenes de datos con un informe, cada uno tiene su propia sección en la página de propiedades. Los orígenes de datos se muestran en el orden en que se definieron en el informe.  
  
 Al especificar un origen de datos que se va a utilizar con un informe, puede utilizar un origen de datos compartido que se cree y administre independientemente de los informes que lo utilizan. Si no desea utilizar un elemento de origen de datos compartido, puede definir la conexión con el origen de datos que se va a utilizar para el informe.  
  
## <a name="navigation"></a>Navegación  
 Utilice el procedimiento siguiente para navegar hasta esta ubicación en la interfaz de usuario (IU).  
  
### <a name="to-open-the-data-sources-properties-page"></a>Para abrir la página de propiedades de orígenes de datos  
  
1.  Abra el Administrador de informes y busque el informe para el que desea seleccionar un origen de datos.  
  
2.  Mantenga el mouse sobre el informe y haga clic en la flecha de lista desplegable.  
  
3.  En el menú desplegable, haga clic en **Administrar**. Se abrirá la página de propiedades **General** correspondiente al informe.  
  
4.  Seleccione la pestaña **Orígenes de datos** .  
  
## <a name="options"></a>Opciones  
 **Un origen de datos compartido**  
 Especifique un origen de datos compartido para utilizarlo con el informe. Para obtener más información acerca de cómo crear un nuevo origen de datos, vea [crear, eliminar o modificar un origen de datos compartido &#40;el Administrador de informes&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md).  
  
 **Examinar**  
 Haga clic en **Examinar** para abrir la página Selección de origen de datos, que se utiliza para seleccionar un origen de datos compartido. Para obtener más información, consulte [página de selección de origen de datos &#40;el Administrador de informes&#41;](../../2014/reporting-services/data-source-selection-page-report-manager.md).  
  
 **Un origen de datos personalizado**  
 Especifique cómo se conecta el informe al origen de datos.  
  
 Para especificar una conexión con un origen de datos personalizado, se utilizan las opciones siguientes.  
  
 **Tipo de origen de datos**  
 Especifique la extensión de procesamiento de datos que se va a utilizar para procesar los datos del origen de datos. Para obtener la lista de extensiones de datos integradas, consulte [orígenes de datos admitidos por Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md). Es posible que otros fabricantes ofrezcan extensiones de procesamiento de datos adicionales.  
  
 **Cadena de conexión**  
 Especifique la cadena de conexión que utiliza el servidor de informes para conectarse al origen de datos. El tipo de conexión determina la sintaxis que debería usar. Por ejemplo, una cadena de conexión para la extensión de procesamiento de datos XML es una dirección URL a un documento XML. En la mayoría de los casos, la cadena de conexión típica especifica el servidor de bases de datos y un archivo de datos. En el siguiente ejemplo, se muestra la cadena de conexión utilizada para conectarse a una base de datos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] denominada MyData:  
  
 `data source=<a SQL Server instance>;initial catalog=MyData`  
  
 La cadena de conexión puede configurarse como expresión para que pueda especificar el origen de datos en tiempo de ejecución. Las expresiones de origen de datos se definen en el informe en el Diseñador de informes. Las expresiones de origen de datos no se pueden definir, ver ni modificar en el Administrador de informes. Sin embargo, una expresión de origen de datos se puede reemplazar haciendo clic en **Reemplazar predeterminado** para escribir una cadena de conexión estática. Si desea recuperar la expresión, haga clic en **Volver al valor predeterminado**. El servidor de informes almacena la cadena de conexión original por si necesita restaurarla. Para usar expresiones de origen de datos, debe usar la información de conexión a un origen de datos que se publicó originalmente en el informe. Los orígenes de datos compartidos no admiten el uso de expresiones en la cadena de conexión.  
  
 **Conectar utilizando**  
 Especifica las opciones que determinan cómo se obtienen las credenciales.  
  
> [!IMPORTANT]  
>  Si las credenciales se suministran en la cadena de conexión, se omiten las opciones y los valores que se proporcionan en esta sección. Tenga en cuenta que, si especifica las credenciales en la cadena de conexión, todos los usuarios que abran esta página verán los valores como texto no cifrado.  
  
 **Credenciales suministradas por el usuario que ejecuta el informe**  
 Cada usuario debe escribir un nombre de usuario y una contraseña para acceder al origen de datos. Puede definir el texto del mensaje que solicita las credenciales del usuario. La cadena de texto predeterminada es "Especifique un nombre de usuario y una contraseña para tener acceso al origen de datos".  
  
 Seleccione **Usar como credenciales de Windows para la conexión al origen de datos** si las credenciales que el usuario suministra son las credenciales de autenticación de Windows. No seleccione esta casilla si está usando la autenticación de base de datos (por ejemplo, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticación).  
  
 **Credenciales almacenadas de forma segura en el servidor de informes**  
 Almacene un nombre de usuario y una contraseña cifrados en la base de datos del servidor de informes. Seleccione esta opción para ejecutar un informe de manera desatendida; por ejemplo, informes iniciados por programaciones o eventos en lugar de una acción del usuario. Si va a usar la seguridad predeterminada, el nombre de usuario debe ser una cuenta de dominio de Windows. Especifique la cuenta con este formato: \<dominio >\\< nombre de usuario\>. La cuenta que especifica debe tener permisos de inicio de sesión local en el equipo que hospeda el origen de datos usado por el informe.  
  
 Active la casilla **Utilizar como credenciales de Windows para la conexión al origen de datos** si las credenciales son las credenciales de autenticación de Windows. No seleccione esta casilla si está usando la autenticación de base de datos (por ejemplo, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] autenticación).  
  
 Seleccione **Suplantar al usuario autenticado después de realizar una conexión al origen de datos** para permitir la delegación de credenciales, pero solo si un origen de datos admite la suplantación. Para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] bases de datos, esta opción establece la función SETUSER.  
  
> [!TIP]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]solo admite credenciales de cuenta de Windows. Por lo tanto, debe seleccionar ambas opciones "Utilizar como credenciales de Windows al conectarse al origen de datos" y "suplantar al usuario autenticado después de realizar una conexión al origen de datos" para un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] origen de datos.  
  
 **Seguridad integrada de Windows**  
 Use las credenciales de Windows del usuario actual para obtener acceso al origen de datos. Seleccione esta opción cuando las credenciales que se usan para obtener acceso a un origen de datos son las mismas que se usaron para iniciar sesión en el dominio de red. Esta opción funciona de manera óptima cuando la autenticación Kerberos está habilitada para el dominio o cuando el origen de datos se encuentra en el mismo equipo que el servidor de informes. Si Kerberos no está habilitado, se pueden pasar las credenciales de Windows a otro equipo. Si se requieren más conexiones de equipos, obtendrá un error en lugar de los datos esperados.  
  
 Un administrador del servidor de informes puede deshabilitar el uso de seguridad integrada de Windows para tener acceso a los orígenes de datos del informe. Si este valor está deshabilitado, la característica no está disponible.  
  
 No use esta opción si piensa programar o suscribirse a este informe. El procesamiento de informes desatendido o programado requiere credenciales que se pueden obtener sin datos proporcionados por el usuario o el contexto de seguridad de un usuario actual. Solo las credenciales almacenadas proporcionan esta capacidad. Por este motivo, el servidor de informes evita que programe el procesamiento de informes o suscripciones si el informe está configurado para el tipo de credencial de seguridad integrada de Windows. Si elige esta opción para un informe al que ya está suscrito o que tiene operaciones programadas, se detendrán las suscripciones y las operaciones programadas.  
  
 **No se necesitan credenciales**  
 Especifique que no se necesitan credenciales para obtener acceso al origen de datos. Tenga en cuenta que, si un origen de datos requiere un inicio de sesión de usuario, esta opción no tendrá ningún efecto. Elija esta opción solo si la conexión al origen de datos no requiere credenciales de usuario.  
  
 Para usar esta opción, debe haber configurado previamente la cuenta de ejecución desatendida para la implementación del servidor de informes. La cuenta de ejecución desatendida se usa para conectarse a los orígenes de datos externos cuando otros orígenes de credenciales no están disponibles. Si especifica esta opción y la cuenta no está configurada, se producirá un error en la conexión al origen de datos del informe y no se producirá el procesamiento de informes.  Para obtener más información acerca de esta cuenta, consulte [configurar la cuenta de ejecución desatendida &#40;SSRS Configuration Manager&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
 **Aplicar**  
 Haga clic para guardar los cambios.  
  
## <a name="see-also"></a>Vea también  
 [Administrar orígenes de datos de informe](report-data/manage-report-data-sources.md)   
 [Especificar información de credenciales y conexión para los orígenes de datos de informes](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Administrador de informes (Ayuda F1)](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
