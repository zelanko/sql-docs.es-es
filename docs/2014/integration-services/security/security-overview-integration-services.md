---
title: Información general sobre seguridad (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- Integration Services, security
- security [Integration Services], about security
- passwords [Integration Services]
- packages [Integration Services], security
- SQL Server Integration Services, security
- SSIS, security
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 01aa0b88-d477-4581-9a3b-2efc3de2b133
caps.latest.revision: 72
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ef095dd196b4deacf7fcd6ade6d2d50d3756d6f6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167136"
---
# <a name="security-overview-integration-services"></a>Información general sobre seguridad (Integration Services)
  La seguridad en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consta de varios niveles que proporcionan un entorno de seguridad rico y flexible. Estos niveles de seguridad incluyen el uso de firmas digitales, propiedades de paquete, roles de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y permisos del sistema operativo. La mayoría de estas características de seguridad pertenecen a las categorías de identidad y control de acceso.  
  
## <a name="identity-features"></a>Características de identidad  
 Si implementa características de identidad en los paquetes, puede lograr el objetivo siguiente:  
  
 **Asegurarse de que solo se abren y se ejecutan paquetes de orígenes de confianza**.  
  
 Para asegurarse de que solamente se abren y se ejecutan paquetes de orígenes de confianza, primero debe identificar el origen de los paquetes. Para ello, firme los paquetes con certificados. De esta forma, al abrir o ejecutar los paquetes, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede comprobar la presencia y la validez de las firmas digitales. Para más información, vea [Identificar el origen de paquetes con firmas digitales](identify-the-source-of-packages-with-digital-signatures.md).  
  
## <a name="access-control-features"></a>Características de control de acceso  
 Si implementa características de identidad en los paquetes, puede lograr el objetivo siguiente:  
  
 **Asegurarse de que solo los usuarios autorizados abren y ejecutan paquetes**.  
  
 Para asegurarse de que solo los usuarios autorizados abren y ejecutan paquetes, debe controlar el acceso a la información siguiente:  
  
-   El contenido de los paquetes, sobre todo si son datos confidenciales.  
  
-   Los paquetes y las configuraciones de paquetes almacenadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Los paquetes y los archivos relacionados, como configuraciones, registros y archivos de punto de comprobación, almacenados en el sistema de archivos.  
  
-   El servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y la información sobre paquetes que muestra dicho servicio en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="controlling-access-to-the-contents-of-packages"></a>Controlar el acceso al contenido de los paquetes  
 Para ayudar a restringir el acceso al contenido de un paquete, puede cifrar el paquete estableciendo su propiedad ProtectionLevel. Puede establecer esta propiedad en el nivel de protección que necesita el paquete. Por ejemplo, en un entorno de desarrollo de equipo, puede cifrar un paquete con una contraseña que solo conozcan los miembros del equipo que trabajan en el paquete.  
  
 Cuando se establece la propiedad ProtectionLevel de un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] detecta automáticamente las propiedades confidenciales y las trata de acuerdo con el nivel de protección especificado para el paquete. Por ejemplo, la propiedad ProtectionLevel de un paquete se establece en un nivel que cifra la información confidencial mediante una contraseña. En este paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] cifra automáticamente los valores de todas las propiedades confidenciales y no mostrará los datos correspondientes a no ser que se proporcione la contraseña correcta.  
  
 Normalmente, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] identifica las propiedades como confidenciales si estas contienen información, como una contraseña o una cadena de conexión, o si corresponden a variables o nodos XML generados por tareas. El que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] considere una propiedad como confidencial dependerá de si el programador del componente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , como un administrador de conexiones o una tarea, ha designado la propiedad como tal. Los usuarios no pueden agregar propiedades a la lista de propiedades consideradas como confidenciales, ni tampoco quitarlas de dicha lista. Si escribe tareas, administradores de conexión o componentes de flujo de datos personalizados, puede especificar qué propiedades debe tratar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como confidenciales.  
  
 Para más información, consulte [Access Control for Sensitive Data in Packages](access-control-for-sensitive-data-in-packages.md).  
  
### <a name="controlling-access-to-packages"></a>Controlar el acceso a los paquetes  
 En una instancia de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , los paquetes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]se pueden guardar en la base de datos msdb o en el sistema de archivos como archivos XML con la extensión de nombre de archivo .dtsx. Para más información, vea [Guardar paquetes](../save-packages.md).  
  
#### <a name="saving-packages-to-the-msdb-database"></a>Guardar paquetes en la base de datos msdb  
 Guardar los paquetes en la base de datos msdb proporciona seguridad en los siguientes niveles: servidor, base de datos y tabla. En la base de datos msdb, los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se almacenan en la tabla sysssispackages. Dado que los paquetes se guardan en las tablas sysssispackages y sysdtspackages de la base de datos msdb, se realiza una copia de seguridad de dichos paquetes de forma automática al crear una copia de seguridad de la base de datos msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los paquetes almacenados en la base de datos msdb también se pueden proteger aplicando los roles de nivel de base de datos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] incluye tres roles fijos de nivel de base de datos db_ssisadmin, db_ssisltduser y db_ssisoperator para controlar el acceso a los paquetes. Se puede asociar un rol de lector y de escritor a cada paquete. También se pueden definir roles personalizados de nivel de base de datos para usarlos en los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Los roles solo se pueden implementar en los paquetes que se guardan en la base de datos msdb en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Roles de Integration Services &#40;servicio SSIS&#41;](integration-services-roles-ssis-service.md).  
  
#### <a name="saving-packages-to-the-file-system"></a>Guardar paquetes en el sistema de archivos  
 Si almacena los paquetes en el sistema de archivos en lugar de en la base de datos msdb, no olvide asegurar los archivos de los paquetes y las carpetas que contienen los archivos de los paquetes.  
  
### <a name="controlling-access-to-files-used-by-packages"></a>Controlar el acceso a los archivos usados por los paquetes  
 Los paquetes configurados para usar configuraciones, puntos de comprobación y registros generan información que se almacena fuera del paquete. Esta información puede ser confidencial y debe protegerse. Los archivos de puntos de comprobación únicamente se pueden guardar en el sistema de archivos, pero las configuraciones y los registros se pueden guardar en el sistema de archivos o en tablas de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Las configuraciones y los registros que se guardan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están sujetos a la configuración de seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero la información guardada en el sistema de archivos requiere una seguridad adicional.  
  
 Para obtener más información, vea [Acceso a los archivos usados por los paquetes](../access-to-files-used-by-packages.md).  
  
#### <a name="storing-package-configurations-securely"></a>Almacenar configuraciones de paquetes de forma segura  
 Las configuraciones de paquetes se pueden guardar en una tabla de una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en el sistema de archivos.  
  
 Las configuraciones se pueden guardar en cualquier base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no solo en la base de datos msdb. Por lo tanto, puede especificar qué base de datos actúa como repositorio de las configuraciones de paquetes. También puede especificar el nombre de la tabla que contendrá las configuraciones; [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] creará la tabla de forma automática con la estructura correcta. Guardar las configuraciones en una tabla permite proporcionar seguridad en tres niveles: servidor, base de datos y tabla. Además, las configuraciones guardadas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se agregan automáticamente a la copia de seguridad al crear una copia de seguridad de la base de datos.  
  
 Si almacena las configuraciones en el sistema de archivos en lugar de en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no olvide asegurar las carpetas que contienen los archivos de configuración de paquetes.  
  
 Para obtener más información acerca de las configuraciones, vea [Package Configurations](../package-configurations.md).  
  
### <a name="controlling-access-to-the-integration-services-service"></a>Controlar el acceso al servicio Integration Services  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa el servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para mostrar los paquetes almacenados. Restrinja el acceso a los equipos que ejecutan el servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para evitar que los usuarios no autorizados tengan acceso a la información sobre los paquetes almacenados en equipos locales y remotos, y obtengan información privada.  
  
 Para más información, vea [Acceso al servicio Integration Services](../access-to-the-integration-services-service.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 La lista siguiente contiene vínculos a temas que muestran cómo realizar una determinada tarea relacionada con la seguridad.  
  
-   [Crear un rol definido por el usuario](../create-a-user-defined-role.md)  
  
-   [Asignar roles de lector y escritor a un paquete](../assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Implementar una directiva de firma estableciendo un valor del Registro](../implement-a-signing-policy-by-setting-a-registry-value.md)  
  
-   [Firmar un paquete mediante un certificado digital](../sign-a-package-by-using-a-digital-certificate.md)  
  
-   [Establecer o cambiar el nivel de protección de los paquetes](../set-or-change-the-protection-level-of-packages.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
