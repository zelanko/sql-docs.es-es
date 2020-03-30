---
title: Actualizar Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
author: Minewiskan
ms.author: owend
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: erikre
ms.openlocfilehash: dbf87499f1bc5c23ae272daa393ef981a97e66d5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68892566"
---
# <a name="upgrade-analysis-services"></a>Actualizar Analysis Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  Es posible actualizar las instancias de Analysis Services a una versión de SQL Server del mismo modo de servidor con el objetivo de aprovechar las características que incorpora la nueva versión, tal y como se describe en [What's New in Analysis Services](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services) (Novedades de Analysis Services).  
  
 Puede actualizar cada instancia de forma local, por separado de otras instancias que se ejecuten en el mismo hardware. Pero la mayoría de los administradores optan por instalar una nueva instancia de la versión más reciente para efectuar pruebas con aplicaciones antes de transferir las cargas de trabajo de producción al nuevo servidor. Pero, en el caso de los servidores de entornos de desarrollo o pruebas, una actualización local puede resultar más práctica.  
  
## <a name="server-upgrade"></a>Actualización de servidores  
 Existen dos enfoques básicos para actualizar servidores y bases de datos:  
  
> [!NOTE]
> Los niveles de compatibilidad de las bases de datos asociadas a un servidor determinado seguirán siendo los mismos, a menos que los cambie manualmente.
   
  
### <a name="in-place-upgrade"></a>Actualización local  
 El proceso de actualización migra automáticamente las bases de datos existentes de la instancia antigua a la instancia nueva. Dado que los metadatos y los datos binarios son compatibles entre las dos versiones, después de actualizar se conservarán los datos y no es necesario migrarlos manualmente.  
  
 Para actualizar una instancia existente, ejecute el programa de instalación y especifique el nombre de la instancia existente como nombre de la nueva instancia.  
  
### <a name="side-by-side-upgrade"></a>Actualización en paralelo  
  
-   Realice copias de seguridad de todas las bases de datos y compruebe que se puedan restaurar. Para obtener más información, vea [Backup and Restore of Analysis Services Databases](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases) (Realizar copias de seguridad y restaurar bases de datos de Analysis Services).  
  
-   Identifique un subconjunto de informes, hojas de cálculo o instantáneas del panel a fin de utilizarlo más adelante como base para confirmar las operaciones del servidor posteriores a la actualización. Si fuera posible, recopile medidas de rendimiento para que pueda llevar a cabo comparaciones utilizando las mismas cargas de trabajo en un servidor actualizado.  
  
-   Instale una nueva instancia de Analysis Services; para ello, elija el mismo modo de servidor (tabular o multidimensional) que tenga la instancia que pretende reemplazar. 
  
     Realice las tareas posteriores a la instalación para configurar los puertos y agregar los administradores del servidor. Para obtener más información, vea [Configuración posterior a la instalación &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/post-install-configuration-analysis-services).  
  
-   Adjunte o restaure cada base de datos.  
  
-   Ejecute DBCC para comprobar la integridad de las bases de datos. Los modelos tabulares se someten a una comprobación más completa, en la que se incluyen pruebas de objetos huérfanos en toda la jerarquía del modelo. En lo que respecta a los modelos multidimensionales, solo se comprueban los índices de partición. Para obtener más información, vea [Comprobador de coherencia de base de datos &#40;DBCC&#41; para bases de datos multidimensionales y tabulares de Analysis Services](https://docs.microsoft.com/analysis-services/instances/database-consistency-checker-dbcc-for-analysis-services).  
  
-   Pruebe los informes, las hojas de cálculo y los paneles para confirmar que no haya ningún cambio adverso en el comportamiento o los cálculos. Debería observar un funcionamiento más rápido tanto para cargas de trabajo multidimensionales como para las tabulares.  
  
-   Pruebe las operaciones de procesamiento y corrija cualquier problema de inicio de sesión o permisos. Si utiliza la cuenta de servicio predeterminada para las conexiones, el nuevo servicio se ejecuta en una cuenta diferente. Para obtener más información, vea [Configurar las cuentas de servicio &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/configure-service-accounts-analysis-services).  
  
-   Pruebe las operaciones de copia de seguridad y restauración en el servidor actualizado ajustando los scripts para que utilicen el nuevo nombre del servidor.  
  
## <a name="database-upgrade"></a>Actualización de bases de datos  
 Las bases de datos creadas en versiones anteriores se ejecutan en el servidor actualizado con la configuración de nivel de compatibilidad original. Por lo general, es posible actualizar una base de datos o un modelo para que funcionen con un nivel de compatibilidad superior a fin de disfrutar de nuevas características, pero tenga presente que, si opta por hacerlo, quedará vinculado a una versión específica del servidor.  
  
 Para actualizar una base de datos, normalmente se actualiza el modelo en SQL Server Data Tools (SSDT) y, después, se implementa la solución en una instancia del servidor actualizada.
  
 Las bases de datos tabulares y multidimensionales siguen rutas de versión distintas. Es una coincidencia que los modelos multidimensionales y tabulares tengan niveles de compatibilidad numerada similares.  Los modos avanzarán a ritmos distintos si los cambios de características solo repercuten en uno de ellos.  
  
 Para ofrecer un poco de contexto, en la siguiente tabla se resumen los niveles de compatibilidad, aunque le recomendamos que lea los artículos detallados para comprender qué ofrece cada nivel.  
  
||||  
|-|-|-|  
|Tabular|1400|SQL Server 2017|
|Tabular|1200|SQL Server 2016|  
|Tabular|1103|SQL Server 2014|  
|Tabular|1100|SQL Server 2012|  
|Multidimensional|1100|SQL Server 2012 y posterior|  
|Multidimensional|1050|SQL Server 2005, 2008 y 2008 R2|  
  
 Para obtener más información, vea [Nivel de compatibilidad de una base de datos multidimensional &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services) y [Nivel de compatibilidad para modelos tabulares de Analysis Services](https://docs.microsoft.com/analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services).  
  
## <a name="see-also"></a>Consulte también  
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Actualización de PowerPivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)   
  
  
