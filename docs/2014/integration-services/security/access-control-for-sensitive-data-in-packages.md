---
title: Control del acceso a la información confidencial en paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- passwords [Integration Services]
- packages [Integration Services], security
- protection levels for packages [Integration Services]
- configuration files [Integration Services]
- encryption [Integration Services]
- cryptography [Integration Services]
- security [Integration Services], protection levels
ms.assetid: d4b073c4-4238-41fc-a258-4e114216e185
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 39c6316a6e256cf7dab161d57a032b777dfac09a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48163635"
---
# <a name="access-control-for-sensitive-data-in-packages"></a>Control del acceso a la información confidencial en paquetes
  Para proteger los datos de un paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , puede establecer un nivel de protección que ayude a proteger los datos confidenciales únicamente o todos los datos del paquete. Asimismo, puede cifrar estos datos con una contraseña o una clave de usuario, o confiar en que la base de datos cifre los datos. Además, el nivel de protección que utiliza para un paquete no es necesariamente estático, sino que cambia a lo largo de su ciclo de vida. A menudo se establece un nivel de protección durante el desarrollo y otro cuando el paquete se implementa.  
  
> [!NOTE]  
>  Además de los niveles de protección descritos en este tema, puede usar roles fijos de nivel de base de datos para proteger los paquetes que se guardan en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
## <a name="definition-of-sensitive-information"></a>Definición de la información confidencial  
 En un paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , la información siguiente se define como *confidencial*:  
  
-   La parte de contraseña de una cadena de conexión. Sin embargo, si elige una opción que cifra todo, la cadena de conexión completa se considerará confidencial.  
  
-   Los nodos XML generados por la tarea y etiquetados como confidenciales. El etiquetado de los nodos XML está controlado por [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los usuarios no lo pueden cambiar.  
  
-   Todas las variables marcadas como confidenciales. El marcado de las variables está controlado por [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 El que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] considere una propiedad como confidencial dependerá de si el programador del componente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , como un administrador de conexiones o una tarea, ha designado la propiedad como tal. Los usuarios no pueden agregar propiedades a la lista de propiedades que se consideran confidenciales, ni pueden quitarlas de la lista.  
  
## <a name="encryption"></a>Cifrado  
 El cifrado, como se usa en los niveles de protección de paquetes, se realiza con la API de protección de datos (DPAPI) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] , que forma parte de la API de criptografía (CryptoAPI).  
  
 Los niveles de protección de paquetes que cifran los paquetes con contraseñas requieren que el usuario también suministre una contraseña. Si cambia el nivel de protección de uno que no utilice contraseñas a otro que sí lo haga, se le pedirá una contraseña.  
  
 Además, para los niveles de protección que usan una contraseña, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa el algoritmo de cifrado Triple DES con una longitud de clave de 192 bits, disponible en la biblioteca de clases de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (FCL).  
  
## <a name="protection-levels"></a>Niveles de protección  
 En la tabla siguiente se describen los niveles de protección que proporciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Los valores entre paréntesis son valores de la enumeración <xref:Microsoft.SqlServer.Dts.Runtime.DTSProtectionLevel> . Estos valores aparecen en la ventana Propiedades que se utiliza para configurar las propiedades del paquete al trabajar con paquetes en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
|Nivel de protección|Descripción|  
|----------------------|-----------------|  
|No guardar la información confidencial (`DontSaveSensitive`)|Suprime los valores de las propiedades confidenciales del paquete al guardarlo. Este nivel de protección no cifra, sino que impide que se guarden con el paquete las propiedades marcadas como confidenciales y, en consecuencia, impide que los datos confidenciales estén disponibles para otros usuarios. Si un usuario distinto abre el paquete, aparecerán espacios en blanco en el lugar de la información confidencial y usuario deberá suministrar la información confidencial.<br /><br /> Cuando se usa con la utilidad **dtutil** (dtutil.exe), este nivel de protección se corresponde con el valor de 0.|  
|Cifrar todo con contraseña (`EncryptAllWithPassword`)|Usa una contraseña para cifrar todo el paquete. El paquete se cifra con una contraseña suministrada por el usuario al crear o exportar el paquete. Para abrir el paquete en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] o ejecutarlo con la utilidad del símbolo del sistema **dtexec** , el usuario debe proporcionar la contraseña del paquete. Sin la contraseña, el usuario no tiene acceso al paquete ni lo puede ejecutar.<br /><br /> Cuando se usa con la utilidad **dtutil** , este nivel de protección corresponde al valor 3.|  
|Cifrar todo con la clave de usuario (`EncryptAllWithUserKey`)|Utiliza una clave que se basa en el perfil de usuario actual para cifrar el paquete entero. El usuario que creó o exportó el paquete es el único que puede abrirlo en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] o ejecutarlo con la utilidad del símbolo del sistema **dtexec** .<br /><br /> Cuando se usa con la utilidad **dtutil** , este nivel de protección corresponde al valor 4.<br /><br /> Nota: Para los niveles de protección que utilizan una clave de usuario, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utiliza los estándares DPAPI. Para obtener más información sobre DPAPI, vea MSDN Library en [http://msdn.microsoft.com/library](http://go.microsoft.com/fwlink/?LinkId=15408).|  
|Cifrar la información confidencial con una contraseña (`EncryptSensitiveWithPassword`)|Utiliza una contraseña para cifrar solamente los valores de las propiedades confidenciales en el paquete. Para el cifrado, se utiliza DPAPI. Los datos confidenciales se guardan como parte del paquete, pero los datos se cifran utilizando una contraseña que el usuario actual suministra al crear o exportar el paquete. Para abrir el paquete en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , el usuario debe proporcionar la contraseña del paquete. Si no se proporciona la contraseña, el paquete se abre sin los datos confidenciales y el usuario actual debe proporcionar valores nuevos para estos datos. Si el usuario intenta ejecutar el paquete sin proporcionar la contraseña, el paquete no se ejecutará. Para obtener más información acerca de las contraseñas y la ejecución desde la línea de comandos, vea [dtexec Utility](../packages/dtexec-utility.md).<br /><br /> Cuando se usa con la utilidad **dtutil** , este nivel de protección corresponde al valor 2.|  
|Cifrar la información confidencial con una clave de usuario (`EncryptSensitiveWithUserKey`)|Utiliza una clave que se basa en el perfil de usuario actual para cifrar solamente los valores de las propiedades confidenciales en el paquete. Solo el mismo usuario que use el mismo perfil puede cargar el paquete. Si un usuario distinto abre el paquete, aparecerán espacios en blanco en el lugar de la información confidencial y usuario actual deberá suministrar valores nuevos para los datos confidenciales. Si el usuario intenta ejecutar el paquete, se generará un error. Para el cifrado, se utiliza DPAPI.<br /><br /> Cuando se usa con la utilidad **dtutil** , este nivel de protección corresponde al valor 1.<br /><br /> Nota: Para los niveles de protección que utilizan una clave de usuario, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] utiliza los estándares DPAPI. Para obtener más información sobre DPAPI, vea MSDN Library en [http://msdn.microsoft.com/library](http://go.microsoft.com/fwlink/?LinkId=15408).|  
|Se basan en el almacenamiento del servidor para el cifrado (`ServerStorage`)|Protege el paquete completo usando roles de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta opción solo se admite cuando se guarda un paquete en la base de datos msdb de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Además, el catálogo de SSISDB emplea el `ServerStorage` nivel de protección<br /><br /> Esta opción no se admite cuando un paquete se guarda en el sistema de archivos desde [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|  
  
## <a name="protection-level-setting-and-the-ssisdb-catalog"></a>Configuración del nivel de protección y el catálogo de SSISDB  
 El catálogo de SSISDB emplea el `ServerStorage` nivel de protección. Al implementar un proyecto de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , el catálogo cifra automáticamente los datos del paquete y los valores confidenciales. El catálogo también descifra automáticamente los datos cuando lo recupera.  
  
 Si exporta el proyecto (archivo .ispac) desde el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] servidor en el sistema de archivos, el sistema cambia automáticamente el nivel de protección para `EncryptSensitiveWithUserKey`. Si importa el proyecto mediante el **Asistente para la integración de servicios de importación proyecto** en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el **ProtectionLevel** propiedad en el **propiedades** ventana muestra un valor de `EncryptSensitiveWithUserKey`.  
  
## <a name="protection-level-setting-based-on-package-life-cycle"></a>Establecimiento del nivel de protección basado en el ciclo de vida de paquetes  
 El nivel de protección de un paquete de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se establece cuando se desarrolla por primera vez en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Posteriormente, al implementar, importar o exportar el paquete desde [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o copiarlo desde [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el Almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] o el sistema de archivos puede actualizar su nivel de protección. Por ejemplo, si crea y guarda los paquetes en un equipo con una de las opciones de nivel de protección de claves de usuario, es probable que necesite cambiar el nivel de protección al entregar el paquete a otros usuarios; de lo contrario, no podrán abrirlo.  
  
 Normalmente, el nivel de protección se cambia como se muestra en los pasos siguientes:  
  
1.  Durante el desarrollo, deje el nivel de protección de los paquetes establecido en el valor predeterminado, `EncryptSensitiveWithUserKey`. Este valor ayuda a asegurarse de que solamente el programador vea los valores confidenciales del paquete. O bien, puede considerar usar `EncryptAllWithUserKey` o `DontSaveSensitive`.  
  
2.  Cuando llegue el momento de implementar los paquetes, tiene que cambiar el nivel de protección por uno que no dependa de la clave de usuario del programador. Por tanto, normalmente tiene que seleccionar `EncryptSensitiveWithPassword` o `EncryptAllWithPassword`. Cifre los paquetes asignando una contraseña segura temporal que también conozca el equipo de operaciones del entorno de producción.  
  
3.  Una vez implementados los paquetes en el entorno de producción, el equipo de operaciones puede volver a cifrar los paquetes implementados asignando una contraseña segura que solo ellos conozcan. O bien, pueden cifrar los paquetes implementados seleccionando `EncryptSensitiveWithUserKey` o `EncryptAllWithUserKey`, y utilizando las credenciales locales de la cuenta que ejecutará los paquetes.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Establecer o cambiar el nivel de protección de los paquetes](../set-or-change-the-protection-level-of-packages.md)  
  
## <a name="see-also"></a>Vea también  
 [Importar y exportar paquetes &#40;servicio SSIS&#41;](../import-and-export-packages-ssis-service.md)   
 [Servicios de integración &#40;SSIS&#41; paquetes](../integration-services-ssis-packages.md)   
 [Información general sobre seguridad &#40;Integration Services&#41;](security-overview-integration-services.md)  
  
  
