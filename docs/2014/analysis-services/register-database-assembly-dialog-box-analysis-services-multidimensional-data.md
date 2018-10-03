---
title: Cuadro de diálogo de ensamblado de base de datos (Analysis Services - datos multidimensionales) registrar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidevstudio.assembly.registerassembly.f1
ms.assetid: 0c07cc87-fc94-456f-b878-7b23e39772b9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3cfc2e55baf9306c34b0e7a88a32ff57d19272e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48075035"
---
# <a name="register-database-assembly-dialog-box-analysis-services---multidimensional-data"></a>Registrar ensamblado de base de datos (cuadro de diálogo) (Analysis Services: datos multidimensionales)
  Use el cuadro de diálogo **Registrar ensamblado de servidor** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para establecer las propiedades de una referencia de ensamblado en una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para mostrar el cuadro de diálogo **Registrar ensamblado de servidor** , haga clic con el botón derecho en la carpeta Ensamblados de una instancia o base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el **Explorador de objetos** y seleccione **Nuevo ensamblado**.  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Tipo**|Seleccione el tipo de referencia de ensamblado. Puede disponer de los siguientes valores:<br /><br /> **Ensamblado .NET**: <br />                      La referencia de ensamblado se refiere a un ensamblado de [!INCLUDE[msCoName](../includes/msconame-md.md)] .NET Framework.<br /><br /> **COM DLL**: <br />                      La referencia de ensamblado se refiere a una biblioteca COM.<br /><br /> <br /><br /> **\*\* Nota de seguridad \* \***  los ensamblados COM pueden suponer un riesgo de seguridad. Debido a esto y a otras consideraciones, los ensamblados COM están en desuso en [!INCLUDE[ssASversion10](../includes/ssasversion10-md.md)]. Es posible que este tipo de ensamblados no esté disponible en versiones futuras.|  
|**Nombre de archivo**|Escriba la ruta de acceso completa y el nombre de archivo del ensamblado .NET o de la biblioteca COM.|  
|**...**|Haga clic para mostrar el cuadro de diálogo **Abrir** y seleccionar la ruta de acceso completa y el nombre de archivo del ensamblado .NET o de la biblioteca COM.|  
|**Nombre del ensamblado**|Escriba el nombre para establecer la referencia de ensamblado.<br /><br /> Nota: Al cambiar este valor no se cambia el nombre del ensamblado al que se refiere la referencia de ensamblado, sino que se cambia el nombre utilizado por la instancia o base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] cuando se refiere a la referencia de ensamblado.|  
|**Incluir información de depuración**|Seleccione esta opción para incluir información de depuración de errores, si la hay, acerca del ensamblado .NET o de la biblioteca COM.|  
|**Marca de tiempo de creación**|Muestra la fecha y la hora de creación de la referencia de ensamblado.|  
|**Última actualización de esquema**|Muestra la fecha y la hora de la última actualización de los metadatos de la referencia de ensamblado.|  
|**Source**|Muestra el origen de la referencia de ensamblado. Esta propiedad normalmente contiene la ruta completa y el nombre de archivo del ensamblado al que se refiere la referencia de ensamblado.|  
|**Seguro**|Seleccione esta opción a fin de utilizar este conjunto de permisos para la referencia de ensamblado. Si se selecciona esta opción, solo se permitirá el acceso a datos locales y el cálculo interno del ensamblado. Todo código ejecutado por un ensamblado que tenga esta opción no podrá obtener acceso a los recursos externos del sistema, como los archivos, la red, las variables de entorno o el Registro.<br /><br /> **\*\* Nota de seguridad \* \***  esta opción es la configuración de permisos recomendada para los ensamblados que realizan tareas de administración de datos y cálculos sin tener acceso a recursos externos a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Esta opción representa el conjunto de permisos con la mayor cantidad de restricciones.|  
|**Acceso externo**|Seleccione esta opción a fin de utilizar este conjunto de permisos para la referencia de ensamblado. Si se selecciona esta opción, solo se permitirá el acceso a datos locales y el cálculo interno del ensamblado. Todo código ejecutado por un ensamblado que tenga este conjunto de permisos podrá obtener acceso a los recursos externos del sistema, como los archivos, las redes, las variables de entorno o el Registro.<br /><br /> **\*\* Nota de seguridad \* \***  se recomienda esta opción para los ensamblados que tienen acceso a recursos externos a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. De manera predeterminada, los ensamblados que utilizan esta opción se ejecutan con las credenciales de seguridad de la cuenta de servicio. Es posible que un código que se encuentre dentro de este ensamblado represente explícitamente el contexto de seguridad de la autenticación de [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows. Debido a que la acción predeterminada es ejecutarse como cuenta de servicio, solo se debe conceder permiso para ejecutar ensamblados con esta opción a roles de confianza para ejecutarse como cuenta de servicio. Esta opción conforma un conjunto de permisos con una menor cantidad de restricciones que **Seguro**, aunque con una mayor cantidad de restricciones que **No restringida**.|  
|**Sin restricciones**|Seleccione esta opción a fin de utilizar este conjunto de permisos para la referencia de ensamblado. Si se selecciona esta opción, el ensamblado tendrá acceso no restringido a los recursos internos y externos. La ejecución de códigos desde el interior de un ensamblado que tenga esta opción puede llamar a un código no administrado.<br /><br /> **\*\* Nota de seguridad \* \***  no se recomienda esta opción a menos que el ensamblado requiera acceso sin restricciones. Desde el punto de vista de la seguridad, esta opción es idéntica a **Acceso externo**. Sin embargo, los ensamblados que utilizan la opción **Acceso externo** proporcionan diferentes protecciones de confiabilidad y solidez que no se incluyen en los ensamblados que usan esta opción. Al especificar esta opción se permite al código del ensamblado realizar operaciones ilegales en el espacio del proceso, lo que podría comprometer la solidez y la escalabilidad de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Esta opción representa el conjunto de permisos con menores restricciones y debe utilizarse con precaución.|  
|**Utilizar un nombre de usuario y una contraseña específicos**|Seleccione esta opción para que el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilice las credenciales de seguridad de una cuenta de usuario especificada.|  
|**Nombre de usuario.**|Escriba el dominio y el nombre de la cuenta de usuario que debe usar el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionado. El dominio y el nombre de la cuenta de usuario tienen el siguiente formato:<br /><br /> *\<Nombre de dominio >* **\\**  *\<nombre de la cuenta de usuario >*<br /><br /> Nota: Esta opción solo está habilitada si está activada la opción **Usar un nombre de usuario y una contraseña específicos** .|  
|**Contraseña**|Escriba el dominio y el nombre de la cuenta de usuario que debe usar el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seleccionado.|  
|**Utilizar cuenta de servicio**|Seleccione esta opción para que el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] use las credenciales de seguridad asociadas al servicio de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que administra el objeto.|  
|**Utilizar las credenciales del usuario actual**|Seleccione esta opción para que el objeto de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilice las credenciales de seguridad del usuario actual.|  
|**Default**|Seleccione esta opción para utilizar la cuenta de usuario predeterminada de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La selección de esta opción equivale a seleccionar la opción **Utilizar las credenciales del usuario actual** .|  
|**Descripción**|Escriba la descripción de la referencia de ensamblado.|  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Administración de los ensamblados de modelos multidimensionales](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
