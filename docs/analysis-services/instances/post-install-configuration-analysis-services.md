---
title: Posterior a la instalación de configuración (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: aadcdb901c39af148b22640413b921aae288f016
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579485"
---
# <a name="post-install-configuration-analysis-services"></a>Configuración posterior a la instalación (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Después de instalar Analysis Services, se necesita cierta configuración adicional para que el servidor sea totalmente operativo y esté disponible para su uso general. En esta sección se presentan las tareas adicionales que completan la instalación. Según los requisitos de conexión, puede ser necesario configurar también la autenticación (vea [Conectar a Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md)).  
  
 Más adelante, será necesario realizar tareas adicionales una vez que tenga bases de datos listas para implementar. Tendrá que configurar las pertenencias a roles de la base de datos para conceder al usuario acceso a los datos, diseñar una estrategia de copia de seguridad y recuperación de la base de datos, y determinar si necesita una carga de trabajo de procesamiento programada para actualizar los datos periódicamente. Para obtener más información sobre la implementación y administración de bases de datos, visite estos vínculos: [Bases de datos modelo multidimensionales](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md) y [bases de datos modelo tabulares](../../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md).  
  
## <a name="instance-configuration"></a>Configuración de instancia  
 Analysis Services es un servicio replicable, lo que significa que puede instalar varias instancias del servicio en un único servidor. Cada instancia adicional se instala por separado como una instancia con nombre, mediante el programa de instalación de SQL Server, y se configura independientemente para admitir su propósito previsto. Por ejemplo, un servidor de desarrollo puede ejecutar Caja negra o usar valores predeterminados para el almacenamiento de datos que de otra forma cambiaría en los servidores que atienden cargas de trabajo de producción. Otro ejemplo que precisa ajustar la configuración del sistema es la instalación de la instancia de Analysis Services en hardware compartido por otros servicios. Cuando se hospedan en el mismo hardware varias aplicaciones que usan muchos datos, puede que desee configurar las propiedades del servidor que reducen los umbrales de memoria para optimizar los recursos disponibles en todas las aplicaciones.  
  
## <a name="post-installation-tasks"></a>Tareas posteriores a la instalación  
  
|Vínculo|Descripción de la tarea|  
|----------|----------------------|  
|[Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Cree una regla de entrada en Firewall de Windows de manera que se puedan enrutar las solicitudes a través del puerto TCP usado por la instancia de Analysis Services. Esta tarea es obligatoria. Nadie puede tener acceso a Analysis Services desde un equipo remoto hasta que no se defina una regla de firewall de entrada.|  
|[Conceder permisos de administrador de servidor (Analysis Services)](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)|Durante la instalación, tenía que agregar al menos una cuenta de usuario al rol Administrador de la instancia de Analysis Services. Los permisos administrativos son necesarios para muchas operaciones rutinarias del servidor, como el procesamiento de datos de bases de datos relacionales externas. Use la información de este tema para agregar o modificar la pertenencia del rol Administrador.|
|[Configurar el software antivirus en equipos que ejecutan SQL Server](https://support.microsoft.com/kb/309422) |Es posible que necesite configurar el software de detección, como aplicaciones antivirus y antispyware, para excluir las carpetas y los tipos de archivo de SQL Server. Si el software de detección bloquea un programa o archivo de datos cuando Analysis Services necesita usarlo, puede producirse una interrupción del servicio o daños en los datos. |
|[Configurar las cuentas de servicio &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)|Durante la instalación, se aprovisionó la cuenta de servicio de Analysis Services con los permisos adecuados para permitir el acceso controlado a los archivos ejecutables de programas y los archivos de base de datos. Como una tarea posterior a la instalación, ahora debe considerar si va a permitir el uso de la cuenta de servicio al realizar tareas adicionales. Tanto las cargas de trabajo de procesamiento como las de consulta se pueden ejecutar bajo la cuenta de servicio. Estas operaciones solo se realizan correctamente cuando la cuenta de servicio tiene los permisos adecuados.|  
|[Registrar una instancia de Analysis Services en un grupo de servidores](../../analysis-services/instances/register-an-analysis-services-instance-in-a-server-group.md)|SQL Server Management Studio (SSMS) permite crear grupos de servidores para organizar las instancias de SQL Server. Las implementaciones escalables que constan de varias instancias de servidor son más fáciles de administrar en grupos de servidores. Use la información de este tema para organizar las instancias de Analysis Services en grupos en SSMS.|  
|[Determinar el modo de servidor de una instancia de Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)|Durante la instalación, elija un modo de servidor que determine el tipo de modelo (multidimensional o tabular) que se ejecuta en el servidor. Si no está seguro del modo de servidor que debe emplear, use la información de este tema para determinar qué modo se instaló.|  
|[Cambiar el nombre de una instancia de Analysis Services](../../analysis-services/instances/rename-an-analysis-services-instance.md)|Un nombre descriptivo puede ayudar a distinguir entre varias instancias que disponen de modos de servidor diferentes, o entre las instancias usadas principalmente por los distintos departamentos o equipos de la organización. Si desea cambiar el nombre de instancia a uno que le ayude a administrar mejor las instalaciones, use la información de este tema para saber cómo hacerlo.|  
  
## <a name="next-steps"></a>Pasos siguientes  
 Aprenda a conectarse a Analysis Services desde aplicaciones de Microsoft o aplicaciones personalizadas mediante las bibliotecas de cliente. En función de los requisitos de la solución, puede ser necesario configurar también el servicio para la autenticación Kerberos. Las conexiones que deben cruzar límites de dominio necesitarán acceso HTTP. Para obtener instrucciones acerca de los pasos siguientes, vea [Connect to Analysis Services](../../analysis-services/instances/connect-to-analysis-services.md) .  
  
## <a name="see-also"></a>Vea también  
 [Instalación de SQL Server 2016](../../database-engine/install-windows/installation-for-sql-server-2016.md)   
 [Instalar Analysis Services en el modo de minería de datos y multidimensional](http://msdn.microsoft.com/library/8a1f33e8-2bd6-4fb8-bd46-c86f2a067f60)   
 [Instalar Analysis Services](../../analysis-services/instances/install-windows/install-analysis-services.md)   
 [Instalación de Analysis Services en el modo PowerPivot](../../analysis-services/instances/install-windows/install-analysis-services-in-power-pivot-mode.md)  
  
  
