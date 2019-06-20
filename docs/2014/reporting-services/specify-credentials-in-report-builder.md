---
title: Especificar credenciales en Generador de informes | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 7412ce68-aece-41c0-8c37-76a0e54b6b53
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 432b41216418cd1ad1bae70557c95a589f5e78dc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66101138"
---
# <a name="specify-credentials-in-report-builder"></a>Especificar credenciales en el Generador de informes
  Las credenciales autentican al usuario que intenta recuperar datos de un origen de datos. El propietario del origen de datos determina el tipo de credenciales que se deben utilizar. Por ejemplo, un administrador de bases de datos podría especificar que el usuario debe proporcionar un nombre de usuario y una contraseña de Windows.  
  
 En una definición de informe, cada definición del origen de datos especifica un nombre, una cadena de conexión, si se va a utilizar la seguridad integrada y el mensaje que se muestra si se requieren credenciales pero no se especifican. Las credenciales no se guardan en la definición de informe. Una vez publicado un informe en el servidor de informes, los orígenes de datos pueden administrarse al margen de una definición de informe. Los propietarios del origen de datos pueden especificar credenciales para orígenes de datos insertados y compartidos en el servidor de informes.  
  
> [!NOTE]  
>  El administrador del servidor de informes debe conceder a los usuarios los permisos adecuados para examinar el servidor de informes con el fin de seleccionar modelos u orígenes de datos compartidos o guardar informes. Para obtener más información, consulte [instalar, desinstalar y asistencia del generador de informes](../../2014/reporting-services/install-uninstall-and-report-builder-support.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
## <a name="understanding-when-credentials-are-used"></a>Cuándo se usan credenciales  
 En el Generador de informes, se suelen usar credenciales al conectarse a un servidor de informes o para las tareas relacionadas con datos, como crear un origen de datos incrustado, ejecutar una consulta del conjunto de datos u ofrecer una vista previa de un informe. Las credenciales no se guardan en el informe. Se administran separadamente en el servidor de informes o en el cliente local. La siguiente lista describe los tipos de credenciales que podría necesitar proporcionar, donde están almacenadas y cómo se utilizan:  
  
-   Las credenciales del servidor de informes que escriba en el [cuadro de diálogo Inicio de sesión de Reporting Services &#40;Generador de informes&#41;](report-builder/reporting-services-login-dialog-box-report-builder.md).  
  
     La primera vez que guarda en, publica en o va a un servidor de informes o un sitio de SharePoint, es posible que necesite escribir sus credenciales. Las credenciales que escribe se utilizan hasta el final de la sesión en el Generador de informes. Si decide guardar las credenciales, se almacenan con seguridad en el equipo junto con su configuración de usuario. En las siguientes sesiones del Generador de informes, se usan las credenciales guardadas para conectar con el mismo servidor de informes o con el sitio de SharePoint. El administrador del servidor de informes o el administrador de SharePoint especifica qué tipo de credenciales hay que utilizar.  
  
-   Las credenciales del origen de datos que escriba en la página [Propiedades del origen de datos (cuadro de diálogo), Credenciales &#40;Generador de informes&#41;](../../2014/reporting-services/data-source-properties-dialog-box-credentials-report-builder.md) de un origen de datos incrustados.  
  
     El servidor de informes utiliza estas credenciales para realizar una conexión de datos al origen de datos externo. Para algunos tipos de orígenes de datos, las credenciales pueden estar almacenadas con seguridad en el servidor de informes. Estas credenciales permiten a otros usuarios ejecutar el informe sin proporcionar las credenciales para la conexión de datos subyacente.  
  
-   Las credenciales del origen de datos que escriba en el [cuadro de diálogo Escribir credenciales de origen de datos &#40;Generador de informes&#41;](report-data/enter-data-source-credentials-dialog-box-report-builder.md) al ejecutar una consulta de conjunto de datos, actualizar campos del conjunto de datos o generar una vista previa del informe.  
  
     Estas credenciales se utilizan para realizar una conexión de datos desde el Generador de informes al origen de datos externo o para ofrecer una vista previa de un informe que se configura para que pida las credenciales. Las credenciales que escribe en este cuadro de diálogo no están almacenadas en el servidor de informes y no están disponible para su uso por otros usuarios. El Generador de informes almacena en memoria caché las credenciales durante la sesión de edición del informe, para que no necesite escribirlas cada vez ejecuta la consulta u ofrece una vista previa del informe.  
  
     Para los orígenes de datos compartidos, utilice la opción **Guardar mi contraseña** para guardar localmente las credenciales con sus valores de usuario en su equipo. El Generador de informes utiliza las credenciales guardadas cada vez que se realiza una conexión al origen de datos externo correspondiente.  
  
 Para más información, vea [Propiedades del origen de datos (cuadro de diálogo), General &#40;Generador de informes&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md) y [Mostrar la vista previa de informes en el Generador de informes](report-builder/previewing-reports-in-report-builder.md).  
  
## <a name="types-of-credentials"></a>Tipos de credenciales  
 El tipo de credenciales que admite un origen de datos lo especifica el propietario del origen de datos. Por ejemplo, para tener acceso a una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , puede ser necesario proporcionar un nombre de usuario y una contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para tener acceso a un origen de datos diferente, puede tener que proporcionar un nombre de usuario y contraseña de Windows. Es posible que algunos orígenes de datos no requieran credenciales.  
  
### <a name="options-for-specifying-credentials"></a>Opciones para especificar credenciales  
 Para especificar credenciales para un origen de datos existen las siguientes opciones:  
  
-   Utilizar el usuario actual de Windows (lo que se conoce también como seguridad integrada).  
  
-   Utilizar un nombre de usuario y una contraseña almacenados.  
  
-   Pedir las credenciales al usuario.  
  
-   No se necesitan credenciales.  
  
### <a name="windows-integrated-security"></a>Seguridad integrada de Windows  
 Al seleccionar **Usar autenticación de Windows (seguridad integrada)** , se pasa el token del usuario actual al origen de datos. En este caso, no se solicita al usuario que escriba un nombre de usuario ni una contraseña. Esta opción requiere normalmente que las características de delegación estén habilitadas. Si estas características no están habilitadas, solamente puede usar esta opción para tener acceso a un origen de datos ubicado en el mismo servidor.  
  
### <a name="user-name-and-password-login"></a>Inicio de sesión con nombre de usuario y contraseña  
 Cuando se selecciona la opción **Usar este nombre de usuario y esta contraseña**, debe especificarse un nombre de usuario y una contraseña para obtener acceso al origen de datos. En el caso de una base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , las credenciales podrían servir para iniciar sesión en la base de datos. Las credenciales se pasan al origen de datos externo para su autenticación.  
  
### <a name="prompted-credentials"></a>Credenciales solicitadas  
 Al especificar las credenciales solicitadas, cada usuario que obtiene acceso al informe debe escribir un nombre de usuario y una contraseña para recuperar los datos. Esta es la opción recomendada para los informes que contienen información confidencial. Las credenciales solicitadas pueden ser para una cuenta de Windows o para iniciar sesión en una base de datos. Si el servidor de bases de datos no reconoce las credenciales proporcionadas, o si al usuario especificado no se le ha concedido permiso para recuperar los datos, se produce un error en la conexión.  
  
### <a name="no-credentials"></a>Sin credenciales  
 No se requieren credenciales para este origen de datos. Para ejecutar este informe en el servidor de informes, se debe configurar una cuenta de ejecución desatendida. Para obtener más información, consulte [configurar la cuenta de ejecución desatendida &#40;SSRS Configuration Manager&#41; ](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) en el [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] documentación en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [libros](https://go.microsoft.com/fwlink/?linkid=121312).  
  
## <a name="see-also"></a>Vea también  
 [Instalar, desinstalar y asistencia del generador de informes](../../2014/reporting-services/install-uninstall-and-report-builder-support.md)   
 [Conexiones de datos u orígenes de datos compartidos e incrustados &#40;Generador de informes y SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Cuadro de diálogo, configuración de opciones del generador de informes &#40;generador de informes&#41;](report-builder/set-default-options-for-report-builder.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md)   
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md)   
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
  
