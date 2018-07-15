---
title: Cambios importantes en Analysis Services las características de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- breaking changes [Analysis Services]
- upgrading Analysis Services
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
caps.latest.revision: 46
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a00010f10148d4ed949a7d5602a68fb6a53b3f6e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37238055"
---
# <a name="breaking-changes-to-analysis-services-features-in-sql-server-2014"></a>Cambios recientes en las características de Analysis Services en SQL Server 2014
  En este tema se describen los principales cambios realizados en [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, los scripts o las funcionalidades basadas en versiones anteriores de SQL Server.  
  
 En este tema:  
  
-   [Cambios importantes en SQL Server 2014](#bkmk_sql2014)  
  
-   [Cambios importantes en SQL Server 2012 SP1](#bkmk_2012Sp1)  
  
-   [Cambios importantes en SQL Server 2012](#bkmk_sql11)  
  
-   [Cambios substanciales de SQL Server 2008 o SQL Server 2008 R2](#bkmk_sql10)  
  
##  <a name="bkmk_sql2014"></a> Cambios recientes en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Hay no hay nuevos cambios principales anunciados para la minería de datos tabulares, multidimensionales, o [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] características de esta versión.  Sin embargo, dado que [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] es tan similar a la [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] versiones, cambios importantes respecto a ambas versiones anteriores se proporcionan aquí por comodidad en caso de que va a actualizar desde [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
##  <a name="bkmk_2012Sp1"></a> Cambios importantes en SQL Server 2012 SP1  
 Se sabe de cambios de código relacionados con la globalización que provocan errores en algunas aplicaciones. Entre los problemas conocidos se incluyen:  
  
 **Distinción de identificadores de objeto**  
 Un cambio de código que pretende hacer que todos los identificadores de objeto no distingan mayúsculas de minúsculas tiene el efecto contrario para algunos idiomas. La intención es que todos los identificadores de objeto no distingan mayúsculas de minúsculas, independientemente de la intercalación. Este cambio alinea Analysis Services con otras aplicaciones que se suelen usar en la misma pila de solución.  
  
 En el caso de idiomas basados en los 26 caracteres del alfabeto latino básico, los identificadores de objeto ahora distinguen mayúsculas de minúsculas, que es el comportamiento deseado.  
  
 En el caso de los alfabetos bicamerales del cirílico y de otros idiomas que usan mayúsculas y minúsculas (griego, armenio y copto), los identificadores de objeto ahora distinguen mayúsculas de minúsculas. Los cambios que provocan errores es más probable que se produzcan cuando existe diferencia de mayúsculas y minúsculas entre un identificador de objeto y la forma en que se hace referencia a él (por ejemplo, un script de procesamiento que hace referencia al identificador de objeto escrito todo en minúsculas). Es probable que este comportamiento cambie en el futuro, pero como solución temporal, se recomienda modificar los scripts para que usen las mismas mayúsculas y minúsculas que el identificador de objeto.  
  
##  <a name="bkmk_sql11"></a> Cambios recientes en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 Esta sección documentan los cambios notificados para [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] las características de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
|Problema|Descripción|  
|-----------|-----------------|  
|Se han quitado comandos de instalación para una instalación de [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)].|El programa de instalación instala [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] pero ya no lo configura. Los comandos de instalación que recopilaban los valores utilizados para las acciones de configuración se han quitado ahora. Entre estos se incluyen /FARMACCOUNT, /FARMPASSWORD, /PASSPHRASE y /FARMADMINPORT.<br /><br /> Si creó scripts de instalación para la instalación desatendida, deberá modificar los scripts para una instalación de [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]. La alternativa es usar los cmdlets de PowerShell para configurar el servidor en modo desatendido. Para obtener más información, consulte [instalar PowerPivot desde el símbolo](../../2014/sql-server/install/install-powerpivot-from-the-command-prompt.md) y [configuración de PowerPivot mediante Windows PowerShell](power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).|  
  
##  <a name="bkmk_sql10"></a> Cambios importantes en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]/[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
 Esta sección contiene los últimos cambios de las versiones anteriores. Si va a actualizar [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], debe revisar los últimos cambios que se realizaron en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] y [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
|Problema|Descripción|  
|-----------|-----------------|  
|La función Exists superficial funciona ahora de manera diferente con conjuntos con nombre que contienen miembros enumerados o combinaciones cruzadas de conjuntos enumerados.|En [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], la función Exists superficial no funcionaba con conjuntos con nombre que contenían miembros enumerados o combinaciones cruzadas de conjuntos enumerados. Para mantener la compatibilidad con el original de la versión versión y SP1 de [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], establezca la propiedad de configuración "ConfigurationSettings\OLAP\Query\NamedSetShallowExistsMode" en 1, o para proporcionar compatibilidad con [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] SP2, establézcala en 2.|  
|Las funciones de VBA tratan los valores nulos y vacíos modo distinto de como se trataban en [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)]|En [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], las funciones de VBA devolvían 0 o una cadena vacía cuando los valores null o valores vacíos se usaban como argumentos. En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], devolverán NULL.|  
|Se producirá un error en el Asistente para la migración porque de forma predeterminada no se instala DSO.|De forma predeterminada, SQL Server 2008 no instala el componente de compatibilidad con versiones anteriores de DSO (Objetos de ayuda a la toma de decisiones). El paquete de compatibilidad con versiones anteriores se instala de forma predeterminada, pero el componente DSO del paquete estará deshabilitado. Puesto que el Asistente para la migración de SQL Server Analysis Services se apoya en este componente, se producirá un error a menos que se instale el componente. Para instalar el componente DSO, haga lo siguiente:<br /><br /> (1) abra el Panel de Control.<br />(2) en Windows XP o Windows Server 2003, seleccione **agregar o quitar programas**. En Windows Vista y Windows Server 2008, seleccione **Programas y características**.<br />(3) con el botón secundario **compatibilidad con versiones anteriores de Microsoft SQL Server 2005**y seleccione **cambio**.<br />(4) en el Asistente para instalación de compatibilidad con versiones anteriores, haga clic en **siguiente**.<br />(5) en la página de mantenimiento del programa, seleccione **modificar**y, a continuación, haga clic en **siguiente**.<br />(6) en la página de selección de características, si Decision Support Objects (DSO) no está disponible, haga clic en la flecha hacia abajo y seleccione **esta característica se instalará en la unidad de disco dura local**. Haga clic en **Siguiente**.<br />(7) en listo para modificar la página del programa, haga clic en **instalar**.<br />8) una vez finalizada la instalación, haga clic en **finalizar**.<br /><br /> <br /><br /> Puede quitar DSO una vez completada la migración siguiendo los pasos anteriores, cambiando la opción para DSO a "**Esta característica no estará disponible**".<br /><br /> Si no se instala el paquete de compatibilidad con versiones anteriores, puede instalarlo desde el soporte de distribución de SQL Server 2008. Observe que hay versiones para cada arquitectura de destino (x86, x64, ia64). Estas versiones se encuentran en las ubicaciones siguientes:<br /><br /> x86\Setup\x86\SQLServer2005_BC.msi<br /><br /> x64\Setup\x64\SQLServer2005_BC.msi<br /><br /> ia64\Setup\ia64\SQLServer2005_BC.msi|  
|No se recomienda colocar la ubicación de la partición en la carpeta de datos.|El servidor administra la carpeta de datos, y crea o quita carpetas cuando se crea, se elimina o se altera algún objeto. Por consiguiente, es muy poco recomendable especificar una ubicación de almacenamiento de partición, especialmente en las subcarpetas para bases de datos, cubos y dimensiones. Aunque el servidor permite hacerlo con Create o Alter, mostrará una advertencia. Al actualizar las bases de datos de SQL Server 2005 Analysis Services para [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services que tengan ubicaciones de almacenamiento de partición en la carpeta de datos, funcionará. La restauración y la sincronización requieren que se muevan las ubicaciones de almacenamiento de partición fuera de la carpeta de datos.|  
|Quizá obtenga resultados inesperados para las consultas que utilicen la palabra clave MDX "EXISTING" en ProClarity Analytics Server y Microsoft Office PerformancePoint Server 2007.|ProClarity Analytics Server y Microsoft Office PerformancePoint Server 2007 utilizan la palabra clave EXISTING en MDX de forma incorrecta en determinados escenarios. Debido a los cambios realizados en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services, estas consultas podrían devolver resultados inesperados.|  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con versiones anteriores de Analysis Services](analysis-services-backward-compatibility.md)  
  
  
