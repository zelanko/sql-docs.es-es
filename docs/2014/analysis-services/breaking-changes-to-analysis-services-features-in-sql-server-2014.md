---
title: Principales cambios en las características de Analysis Services en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- breaking changes [Analysis Services]
- upgrading Analysis Services
ms.assetid: aeb02542-5a6c-458c-a110-13413dd3e9d9
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4d6aac37a1287e597f1c34936e8aae4af8571aa5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527841"
---
# <a name="breaking-changes-to-analysis-services-features-in-sql-server-2014"></a>Cambios recientes en las características de Analysis Services en SQL Server 2014
  En este tema se describen los principales cambios realizados en [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, los scripts o las funcionalidades basadas en versiones anteriores de SQL Server.  
  
 En este tema:  
  
-   [Principales cambios en SQL Server 2014](#bkmk_sql2014)  
  
-   [Cambios que provocan errores en SQL Server 2012 SP1](#bkmk_2012Sp1)  
  
-   [Principales cambios en SQL Server 2012](#bkmk_sql11)  
  
-   [Cambios importantes en SQL Server 2008/SQL Server 2008 R2](#bkmk_sql10)  
  
##  <a name="breaking-changes-in-sssql14"></a><a name="bkmk_sql2014"></a>Principales cambios en[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 No hay cambios principales anunciados para la minería de datos tabulares, multidimensionales o para las características de [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] de esta versión.  Sin embargo, como  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] es tan similar a las versiones [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] , se proporcionan cambios principales en ambas versiones anteriores por comodidad, en caso de que se esté actualizando desde [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
##  <a name="breaking-changes-in-sql-server-2012-sp1"></a><a name="bkmk_2012Sp1"></a>Cambios importantes en SQL Server 2012 SP1  
 Se sabe de cambios de código relacionados con la globalización que provocan errores en algunas aplicaciones. Entre los problemas conocidos se incluyen:  
  
 **Distinción de mayúsculas y minúsculas de los identificadores de objeto**  
 Un cambio de código que pretende hacer que todos los identificadores de objeto no distingan mayúsculas de minúsculas tiene el efecto contrario para algunos idiomas. La intención es que todos los identificadores de objeto no distingan mayúsculas de minúsculas, independientemente de la intercalación. Este cambio alinea Analysis Services con otras aplicaciones que se suelen usar en la misma pila de solución.  
  
 En el caso de idiomas basados en los 26 caracteres del alfabeto latino básico, los identificadores de objeto ahora distinguen mayúsculas de minúsculas, que es el comportamiento deseado.  
  
 En el caso de los alfabetos bicamerales del cirílico y de otros idiomas que usan mayúsculas y minúsculas (griego, armenio y copto), los identificadores de objeto ahora distinguen mayúsculas de minúsculas. Los cambios que provocan errores es más probable que se produzcan cuando existe diferencia de mayúsculas y minúsculas entre un identificador de objeto y la forma en que se hace referencia a él (por ejemplo, un script de procesamiento que hace referencia al identificador de objeto escrito todo en minúsculas). Es probable que este comportamiento cambie en el futuro, pero como solución temporal, se recomienda modificar los scripts para que usen las mismas mayúsculas y minúsculas que el identificador de objeto.  
  
##  <a name="breaking-changes-in-sssql11"></a><a name="bkmk_sql11"></a>Principales cambios en[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 En esta sección se documentan los cambios importantes notificados de las características de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
|Problema|Descripción|  
|-----------|-----------------|  
|Comandos de instalación quitados de una instalación de [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] .|El programa de instalación instala [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]pero ya no lo configura. Los comandos de instalación que recopilaban los valores utilizados para las acciones de configuración se han quitado ahora. Entre estos se incluyen /FARMACCOUNT, /FARMPASSWORD, /PASSPHRASE y /FARMADMINPORT.<br /><br /> Si creó scripts de instalación para la instalación desatendida, deberá modificar los scripts para una instalación de [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)] . La alternativa es usar los cmdlets de PowerShell para configurar el servidor en modo desatendido. Para obtener más información, vea [instalar PowerPivot desde el símbolo del sistema y la](../../2014/sql-server/install/install-powerpivot-from-the-command-prompt.md) configuración de [PowerPivot mediante Windows PowerShell](power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md).|  
  
##  <a name="breaking-changes-in-sskatmaisskilimanjaro"></a><a name="bkmk_sql10"></a>Principales cambios en[!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]/[!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]  
 Esta sección contiene los últimos cambios de las versiones anteriores. Si va a actualizar [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], debe revisar los últimos cambios que se realizaron en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] y [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
|Problema|Descripción|  
|-----------|-----------------|  
|La función Exists superficial funciona ahora de manera diferente con conjuntos con nombre que contienen miembros enumerados o combinaciones cruzadas de conjuntos enumerados.|En [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], la función Exists superficial no funcionaba con conjuntos con nombre que contenían miembros enumerados o combinaciones cruzadas de conjuntos enumerados. Para mantener la compatibilidad con la versión original y con el Service Pack 1 de [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], establezca la propiedad de configuración "ConfigurationSettings\OLAP\Query\NamedSetShallowExistsMode" en 1; para mantener la compatibilidad con el Service Pack 2 de [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)] , establezca la propiedad en 2.|  
|Las funciones de VBA tratan los valores NULL y los valores vacíos de un modo distinto de como se trataban en [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)].|En [!INCLUDE[ssASversion2005](../includes/ssasversion2005-md.md)], las funciones de VBA devolvían 0 o una cadena vacía cuando se usaban como argumentos valores NULL o valores vacíos. En [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], devolverán NULL.|  
|Se producirá un error en el Asistente para la migración porque de forma predeterminada no se instala DSO.|De forma predeterminada, SQL Server 2008 no instala el componente de compatibilidad con versiones anteriores de DSO (Objetos de ayuda a la toma de decisiones). El paquete de compatibilidad con versiones anteriores se instala de forma predeterminada, pero el componente DSO del paquete estará deshabilitado. Puesto que el Asistente para la migración de SQL Server Analysis Services se apoya en este componente, se producirá un error a menos que se instale el componente. Para instalar el componente DSO, haga lo siguiente:<br /><br /> 1) Abra el panel de control.<br />2) en Windows XP o Windows Server 2003, seleccione **Agregar o quitar programas**. En Windows Vista y Windows Server 2008, seleccione **Programas y características**.<br />3) haga clic con el botón derecho en **Microsoft SQL Server 2005 compatibilidad con versiones anteriores**y seleccione **cambiar**.<br />4) en el Asistente para la instalación de compatibilidad con versiones anteriores, haga clic en **siguiente**.<br />5) en la página mantenimiento del programa, seleccione **modificar**y, a continuación, haga clic en **siguiente**.<br />6) en la página selección de características, si objetos de ayuda para la toma de decisiones (DSO) no está disponible, haga clic en la flecha hacia abajo y seleccione **esta característica se instalará en la unidad de disco duro local**. Haga clic en **Next**.<br />7) en la página listo para modificar el programa, haga clic en **instalar**.<br />8) cuando haya finalizado la instalación, haga clic en **Finalizar**.<br /><br /> <br /><br /> Puede quitar DSO una vez completada la migración siguiendo los pasos anteriores, cambiando la opción para DSO a "**esta característica no estará disponible**".<br /><br /> Si no se instala el paquete de compatibilidad con versiones anteriores, puede instalarlo desde el soporte de distribución de SQL Server 2008. Observe que hay versiones para cada arquitectura de destino (x86, x64, ia64). Estas versiones se encuentran en las ubicaciones siguientes:<br /><br /> x86\Setup\x86\SQLServer2005_BC.msi<br /><br /> x64\Setup\x64\SQLServer2005_BC.msi<br /><br /> ia64\Setup\ia64\SQLServer2005_BC.msi|  
|No se recomienda colocar la ubicación de la partición en la carpeta de datos.|El servidor administra la carpeta de datos, y crea o quita carpetas cuando se crea, se elimina o se altera algún objeto. Por consiguiente, es muy poco recomendable especificar una ubicación de almacenamiento de partición, especialmente en las subcarpetas para bases de datos, cubos y dimensiones. Aunque el servidor permite hacerlo con Create o Alter, mostrará una advertencia. Cuando actualice bases de datos de SQL Server 2005 Analysis Services a [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services que tengan ubicaciones de almacenamiento de partición en la carpeta de datos, funcionará. La restauración y la sincronización requieren que se muevan las ubicaciones de almacenamiento de partición fuera de la carpeta de datos.|  
|Quizá obtenga resultados inesperados para las consultas que utilicen la palabra clave MDX "EXISTING" en ProClarity Analytics Server y Microsoft Office PerformancePoint Server 2007.|ProClarity Analytics Server y Microsoft Office PerformancePoint Server 2007 utilizan la palabra clave EXISTING en MDX de forma incorrecta en determinados escenarios. Debido a los cambios realizados en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] Analysis Services, estas consultas podrían devolver resultados inesperados.|  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con versiones anteriores Analysis Services](analysis-services-backward-compatibility.md)  
  
  
