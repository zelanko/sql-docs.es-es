---
title: Proteger informes y recursos | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- security [Reporting Services], reports
- security [Reporting Services], resources
- reports [Reporting Services], security
- confidential reports [Reporting Services]
- resources [Reporting Services], security
ms.assetid: 63cd55c7-fd2a-49e3-a3f8-59eb1a1c6e83
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 66e32b412558ec3c06fcbfcb3b4dbd1b7b2e06e0
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="secure-reports-and-resources"></a>Proteger informes y recursos
  Puede establecer la seguridad para informes y recursos individuales a fin de controlar el grado de acceso de los usuarios a estos elementos. De manera predeterminada, solo los usuarios que pertenezcan al grupo integrado **Administradores** pueden ejecutar informes, ver recursos, modificar propiedades y eliminar elementos. Para los demás usuarios se deben crear asignaciones de roles que concedan acceso a un informe o recurso.  
  
## <a name="role-based-access-to-reports-and-resources"></a>Acceso a informes y recursos basado en roles  
 Para concecer acceso a informes y recursos, puede permitir que los usuarios hereden las asignaciones de roles existentes en una carpeta primaria o crear una nueva asignación de rol en el propio elemento.  
  
 Es posible que en la mayoría de los casos se usen los permisos heredados de una carpeta primaria. Establezca la seguridad en un informe o recurso individual solamente si desea ocultar el informe o el recurso a los usuarios que no necesitan saber que existe, o para aumentar el nivel de acceso para un informe o elemento. Estos objetivos no se excluyen mutuamente. Puede restringir el acceso a un informe a un conjunto más reducido de usuarios y proporcionar a todos o a parte de ellos privilegios adicionales para administrar el informe.  
  
 Es posible que necesite crear varias asignaciones de roles para lograr sus objetivos. Por ejemplo, supongamos que tiene un informe que desea poner a disposición de los usuarios Ana y Pablo, y del grupo Directores de recursos humanos. Ana y Pablo deben ser capaces de administrar el informe, pero los miembros de Directores de recursos humanos solo necesitan ejecutarlo. Para adaptarse a todos estos usuarios, deberá crear tres asignaciones de roles diferentes: una para convertir a Ana en administradora de contenido del informe, otra para convertir a Pablo en administrador de contenido del informe y una última para permitir tareas de solo vista al grupo Directores de recursos humanos.  
  
 Una vez que haya establecido la seguridad para un informe o recurso, esta configuración permanecerá con el elemento incluso si lo mueve a otra ubicación. Por ejemplo, si mueve un informe al que solo varias personas están autorizadas a tener acceso, el informe continúa estando disponible solamente para esos usuarios, incluso si lo mueve a una carpeta con una directiva de seguridad relativamente abierta.  
  
## <a name="mitigating-html-injection-attacks-in-a-published-report-or-document"></a>Mitigar los ataques por inyección de código HTML en un informe o documento publicado  
 En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], los informes y recursos se procesan con la identidad de seguridad del usuario que ejecuta el informe. Si el informe contiene expresiones, script, elementos de informe personalizados o ensamblados personalizados, el código se ejecuta con las credenciales del usuario. Si un recurso es un documento HTML que contiene script, éste se ejecutará cuando el usuario abra el documento en el servidor de informes. La posibilidad de ejecutar script o código en un informe es una característica relevante, pero conlleva ciertos riesgos. Si el código es malintencionado, el servidor de informes y el usuario que ejecuta el informe son vulnerables a los ataques.  
  
 A la hora de conceder acceso a los informes y recursos que se procesan como HTML, es importante recordar que los informes se procesan con plena confianza y que puede enviarse al cliente script posiblemente malintencionado. El cliente ejecutará el código HTML en el nivel de confianza que se haya configurado en el explorador.  
  
 Para mitigar el riesgo de ejecutar script malintencionado, tome las siguientes precauciones:  
  
-   Sea selectivo a la hora de decidir quién puede publicar contenido en un servidor de informes. Dado que existe la posibilidad de que se publique contenido malintencionado, debe limitar los usuarios que pueden publicar contenido a un pequeño número de usuarios de confianza.  
  
-   Todos los publicadores deben evitar publicar informes y recursos que procedan de fuentes desconocidas o que no sean de confianza. Si es necesario, abra el archivo en un editor de texto y compruebe si hay script y direcciones URL sospechosos.  
  
## <a name="report-parameters-and-script-injection"></a>Parámetros de informe e inyección de script  
 Los parámetros de informe proporcionan la flexibilidad para todo el diseño y ejecución del informe. Sin embargo, esta misma flexibilidad puede, en algunos casos, ser usada para atraer ataques por señuelo. Para reducir el riesgo de ejecución accidental de scripts malintencionados, abra los informes representados exclusivamente desde orígenes de confianza. Se recomienda que considere el siguiente escenario que es un ataque potencial de inyección de script de representación HTML:  
  
1.  Un informe contiene un cuadro de texto con la acción de hipervínculo establecida en el valor de un parámetro que podría contener texto malintencionado.  
  
2.  El informe se publica en un servidor de informes o se hace disponible de cualquier otra forma de manera que el valor del parámetro del informe se puede controlar desde la URL de una página web.  
  
3.  Un atacante crea un vínculo a la página web o el servidor de informes especifica el valor del parámetro con el formato "javascript:\<script malintencionado aquí >" y envía ese vínculo a una persona de un ataque por señuelo.  
  
## <a name="mitigating-script-injection-attacks-in-a-hyperlink-in-a-published-report-or-document"></a>Mitigar los ataques con inyección de scripts en hipervínculos en un informe publicado o documento  
 Los informes pueden contener hipervínculos incrustados en el valor de la propiedad Action en un elemento de informe o parte de un elemento de informe. Los hipervínculos se pueden enlazar a datos que se recuperan de un origen de datos externo cuando se procesa el informe. Si un usuario malintencionado modifica los datos subyacentes, el hipervínculo podría hacer peligroso el scripting. Si un usuario hace clic en el vínculo en el informe publicado o exportado, podrían ejecutarse scripts malintencionados.  
  
 Para mitigar el riesgo de incluir vínculos en un informe que inadvertidamente ejecuten script malintencionado, enlace solo hipervínculos a datos de fuentes de confianza. Compruebe que los datos de los resultados de la consulta y las expresiones que enlazan los datos con los hipervínculos no crean vínculos de los que se pueda sacar provecho negativo. Por ejemplo, no base un hipervínculo en una expresión que concatena los datos de varios campos de conjunto de datos. Si es necesario, vaya al informe y use "Ver origen" para comprobar scripts sospechosos y URLS.  
  
## <a name="mitigating-sql-injection-attacks-in-a-parameterized-report"></a>Mitigar los ataques por inyección de código SQL en un informe con parámetros  
 En cualquier informe que incluya un parámetro de tipo **String**, use una lista de valores disponibles (también conocida como lista de valores válidos) y asegúrese de que los usuarios que ejecuten el informe solamente dispongan de los permisos necesarios para ver los datos del mismo. Cuando se define un parámetro de tipo **String**, el usuario ve un cuadro de texto que admite cualquier valor. Una lista de valores disponibles limita los valores que se pueden especificar. Si el parámetro de informe está asociado a un parámetro de consulta y no se utiliza una lista de valores disponibles, un usuario del informe podría escribir sintaxis SQL en el cuadro de texto y exponer el informe y el servidor a un ataque por inyección de código SQL. Si el usuario tiene permisos suficientes para ejecutar la nueva instrucción SQL, podría provocar resultados no deseados en el servidor.  
  
 Si un parámetro de informe no está asociado a un parámetro de consulta y los valores de parámetro están incluidos en el informe, un usuario del informe podría escribir sintaxis de expresiones o una dirección URL en el valor de parámetro y representar el informe en Excel o HTML. Si, posteriormente, otro usuario visualiza el informe y hace clic en el contenido del parámetro representado, el usuario podría ejecutar accidentalmente el script o el vínculo malintencionados.  
  
 Para reducir el riesgo de ejecución accidental de scripts malintencionados, abra los informes representados exclusivamente desde orígenes de confianza.  
  
> [!NOTE]  
>  En versiones anteriores de la documentación, se incluía un ejemplo de cómo crear una consulta dinámica como una expresión. Este tipo de consulta genera vulnerabilidad a los ataques por inyección de código SQL y, por lo tanto, no se recomienda.  
  
## <a name="securing-confidential-reports"></a>Proteger informes confidenciales  
 Los informes que contienen información confidencial deberían protegerse en el nivel de acceso a datos requiriendo que los usuarios proporcionen credenciales para tener acceso a datos confidenciales. Para más información, consulte [Specify Credential and Connection Information for Report Data Sources](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md). También puede proteger una carpeta para que no resulte accesible a usuarios no autorizados. Para obtener más información, vea [Proteger carpetas](../../reporting-services/security/secure-folders.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar asignaciones de roles](../../reporting-services/security/create-and-manage-role-assignments.md)   
 [Configurar el acceso al Generador de informes](../../reporting-services/report-server/configure-report-builder-access.md)   
 [Conceder permisos en un servidor de informes en modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)   
 [Proteger elementos de orígenes de datos compartidos](../../reporting-services/security/secure-shared-data-source-items.md)   
 [Almacenamiento de las credenciales en un origen de datos de Reporting Services](../../reporting-services/report-data/store-credentials-in-a-reporting-services-data-source.md)  
  
  
