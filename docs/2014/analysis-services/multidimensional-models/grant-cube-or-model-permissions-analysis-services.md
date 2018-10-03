---
title: Conceder permisos para cubos o modelos (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.cubes.f1
helpviewer_keywords:
- user access rights [Analysis Services], cubes
- cubes [Analysis Services], security
- read/write permissions
- permissions [Analysis Services], cubes
ms.assetid: 55b1456e-2f6b-4101-b316-c926f40304e3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44159dccd8fd912e0ebee75c5ab7d1a72c946e75
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149715"
---
# <a name="grant-cube-or-model-permissions-analysis-services"></a>Otorgar permisos para cubos o modelos (Analysis Services)
  Un cubo o modelo tabular es el objeto de consulta principal en un modelo de datos de Analysis Services. Cuando se conecte a datos multidimensionales o tabulares desde Excel para una exploración de datos ad hoc, los usuarios por lo general comienzan seleccionando un cubo o modelo tabular específico como la estructura de datos que subyace tras el objeto de informe dinámico. En este tema, se describe cómo otorgar los permisos necesarios para tener acceso a cubos o datos tabulares.  
  
 De forma predeterminada, ninguna persona que no sea un administrador de servidor o de base de datos dispondrá de permisos para consultar cubos en una base de datos. El acceso a cubos por parte de una persona que no sea administrador requiere pertenecer a un rol que se haya creado para la base de datos que contenga el cubo correspondiente. La pertenencia es compatible con cuentas de usuario o grupo de Windows que se hayan definido en Active Directory o en el equipo local. Antes de comenzar, identifique a qué cuentas se asignará pertenencia en los roles que va a crear.  
  
 Si se tiene acceso de `Read` a un cubo, también se tendrán permisos para las dimensiones, los grupos de medida y las perspectivas que contenga. La mayoría de los administradores otorgarán permisos en el nivel del cubo y, después, restringirán los permisos para objetos específicos, datos asociados o según la identidad del usuario.  
  
 Para preservar las definiciones de roles respecto a implementaciones de soluciones sucesivas, uno de los procedimientos recomendados es definir roles en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] como parte integrante del modelo y, después, que un administrador de bases de datos asigne pertenencias a roles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tras haber publicado la base de datos. Pero también puede usar cualquiera de las herramientas para ambas tareas. Para que este ejercicio sea más sencillo, usaremos [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para las definiciones de rol y para la pertenencia.  
  
> [!NOTE]  
>  Solamente los administradores de servidor o de base de datos con permisos de Control total pueden implementar cubos a partir de archivos de origen en un servidor o crear roles y asignar miembros. Consulte [conceder permisos de administrador de servidor &#40;Analysis Services&#41; ](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md) y [conceder permisos de base de datos &#40;Analysis Services&#41; ](grant-database-permissions-analysis-services.md) para obtener más información acerca de estos permisos niveles.  
  
#### <a name="step-1-create-the-role"></a>Paso 1: Creación del role  
  
1.  En SSMS, conéctese a Analysis Services. Vea [Conectarse desde aplicaciones cliente &#40;Analysis Services&#41;](../instances/connect-from-client-applications-analysis-services.md) si necesita ayuda con este paso.  
  
2.  Abra la carpeta **Bases de datos** en el Explorador de objetos y seleccione una base de datos.  
  
3.  Haga clic con el botón derecho en **Roles** y elija **Nuevo rol**. Tenga en cuenta que los roles se crean en el nivel de la base de datos y se aplican a los objetos que esta contiene. No puede compartir roles entre bases de datos.  
  
4.  En el panel **General** , escriba un nombre y, si lo desea, una descripción. Este panel también contiene diversos permisos de base de datos, como Control total, Procesar base de datos y Leer definición. No se necesita ninguno de estos permisos para consultar un cubo o un modelo tabular. Para más información sobre estos permisos, vea [Otorgar permisos de base de datos &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md).  
  
5.  Proceda con el siguiente paso después de especificar un nombre y una descripción opcional.  
  
#### <a name="step-2-assign-membership"></a>Paso 2: Asignación de la pertenencia  
  
1.  En el panel **Pertenencia** , haga clic en **Agregar** para especificar las cuentas de usuario o grupo de Windows que van a tener acceso al cubo con este rol. Analysis Services solo es compatible con identidades de seguridad de Windows. Tenga en cuenta que en este paso no va a crear inicios de sesión de base de datos. En Analysis Services, los usuarios se conectan a través de cuentas Windows.  
  
2.  Proceda con el paso siguiente para establecer los permisos de los cubos.  
  
     Tenga en cuenta que va a omitir el panel Origen de datos. La mayoría de los consumidores habituales de datos de Analysis Services no necesitan permisos para el objeto de origen de datos. Para más información sobre estos niveles de permisos, vea [Grant permissions on a data source object &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md) .  
  
#### <a name="step-3-set-cube-permissions"></a>Paso 3: Establecimiento de los permisos de los cubos  
  
1.  En el **cubos** panel, seleccione un cubo y, a continuación, haga clic en `Read` o **lectura/escritura** acceso.  
  
     `Read` acceso es suficiente para la mayoría de las operaciones. **Lectura y escritura** solo se usa para reescribir y no para procesar. Para obtener más información acerca de esta capacidad, vea [Set Partition Writeback](set-partition-writeback.md) .  
  
     Tenga en cuenta que puede seleccionar varios cubos, así como otros objetos disponibles en el cuadro de diálogo Crear rol. Cuando se otorgan permisos a un cubo, se está autorizando el acceso a dimensiones y perspectivas asociadas con el cubo. No es necesario agregar manualmente objetos que ya estén representados en el cubo.  
  
     Si necesita modificar la autorización según los objetos o los usuarios, por ejemplo para hacer que ciertas medidas no estén disponibles, puede permitir o denegar el acceso de forma automática a objetos específicos, incluso en las celdas. Para más información, vea [Conceder acceso personalizado a datos de dimensión &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) y [Otorgar acceso personalizado a los datos de las celdas &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md).  
  
2.  Llegados a este punto, después de hacer clic en **Aceptar**todos los miembros de este rol tendrán acceso a los cubos en los niveles de permiso que hubiera especificado.  
  
     Tenga en cuenta que en el panel **Cubos** , puede otorgar permiso a los usuarios para que creen cubos locales desde un cubo del servidor mediante **Obtención de detalles y cubo local**o solamente permitir la obtención de detalles mediante el permiso **Obtención de detalles** .  
  
     Por último, con este panel podrá otorgar derechos de **Procesar base de datos** en el cubo para otorgar a todos los miembros de este rol la capacidad para procesar datos para este cubo. Dado que el procesamiento es, por lo general, una operación restringida, se recomienda dejar la tarea a los administradores o definir roles independientes específicamente para ella. Para más información sobre procedimientos recomendados de proceso de servicios, vea [Otorgar permisos de procesamiento &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md).  
  
#### <a name="step-4-test"></a>Paso 4: Prueba  
  
1.  Use Excel para probar los permisos de acceso a cubos. También puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]con la misma técnica que describimos abajo (ejecutar la aplicación como un usuario que no es administrador).  
  
    > [!NOTE]  
    >  Si es administrador de Analysis Services, los permisos de administrador se combinarán con los roles que tienen menos permisos, de forma que resultará más complicado probar los permisos de rol de forma aislada. Para hacer más sencilla la labor de las pruebas, se recomienda abrir una segunda instancia de SSMS con la cuenta que se ha asignado al rol que está probando.  
  
2.  Mantenga presionada la tecla Mayúsculas y haga clic con el botón derecho en el acceso directo **Excel** para acceder a la opción **Ejecutar como otro usuario** . Especifique una de las cuentas de usuario o grupo de Windows con pertenencia a este rol.  
  
3.  Cuando se abra Excel, use la pestaña Datos para conectarse a Analysis Services. Dado que está ejecutando Excel como un usuario diferente de Windows, la opción **Utilizar autenticación de Windows** es el tipo de credencial correcto que se debe usar cuando se hacen pruebas a los roles. Vea [Conectarse desde aplicaciones cliente &#40;Analysis Services&#41;](../instances/connect-from-client-applications-analysis-services.md) si necesita ayuda con este paso.  
  
     Si se producen errores en la conexión, compruebe la configuración del puerto para Analysis Services y compruebe que el servidor acepta las conexiones remotas. Para obtener información acerca de la configuración del puerto, vea [Configurar Firewall de Windows para permitir el acceso a Analysis Services](../instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) .  
  
#### <a name="step-5-script-role-definition-and-assignments"></a>Paso 5: Definición y asignaciones del rol con el script  
  
1.  El último paso es generar un script que contenga la definición del rol que acaba de crear.  
  
     Si se vuelve a implementar un proyecto desde [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] , se sobrescribirán los roles o pertenencias a roles que no se hayan definido dentro del proyecto. La forma más rápida de volver a generar roles y pertenencias a rol después de volver a realizar una implementación es a través de un script.  
  
2.  En SSMS, vaya a la carpeta **Roles** y haga clic con el botón derecho en un rol existente.  
  
3.  Seleccione **Incluir rol como** | **CREATE TO** | **archivo**.  
  
4.  Guarde el archivo con una extensión de archivo .xmla. Para probar el script, elimine el rol actual, abra el archivo en SSMS y presione F5 para ejecutar el script.  
  
## <a name="next-step"></a>Paso siguiente  
 Puede refinar los permisos de los cubos para restringir el acceso a celdas o datos de dimensiones. Para más información, vea [Conceder acceso personalizado a datos de dimensión &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md) y [Otorgar acceso personalizado a los datos de las celdas &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Metodologías de autenticación admitidas por Analysis Services](../instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Conceder permisos en las estructuras de minería de datos y modelos &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [Conceder permisos en un objeto de origen de datos &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
