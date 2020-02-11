---
title: Realizar una evaluación a petición mediante Explorador de objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d2aadd055334c7ee64871c2fdfe5239c9849e90
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68210944"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>Realizar una evaluación a petición usando Explorador de objetos
  En esta tarea, utilizará el Explorador de objetos para realizar una evaluación a petición de las directivas de prácticas recomendadas para [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] en una instancia única de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  También puede evaluar las directivas en una instancia única a través de servidores registrados. Para obtener más información, consulte [realizar una evaluación a petición mediante el uso de servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Esta lección se basa en la versión de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Para realizar una evaluación a petición de las directivas de prácticas recomendadas en las instancias [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]que ejecutan, debe usar el procedimiento del tema [realizar una evaluación a petición mediante el uso de servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>Realizar una evaluación a petición usando Explorador de objetos  
  
1.  Inicie [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]y después conéctese a [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  En Explorador de objetos, expanda **Administración**, expanda **Administración de directivas**, haga clic con el botón secundario en **directivas**y, a continuación, haga clic en **evaluar**.  
  
    > [!NOTE]  
    >  De forma predeterminada, la instancia local se utiliza como el origen de las directivas. Si ha importado las directivas de prácticas recomendadas previamente, se enumerarán junto con cualquier otra directiva que haya creado. Puede seleccionar cualquiera de las directivas de procedimientos recomendados importados y, a continuación, hacer clic en **evaluar**. Si no ha importado las directivas de prácticas recomendadas, continúe con este procedimiento.  
  
3.  En el cuadro de diálogo **evaluar directivas** , junto al cuadro **origen** , haga clic en el botón de puntos suspensivos (**...**).  
  
4.  En el cuadro de diálogo **Seleccionar origen** , puede seleccionar **archivos** o **servidor** como origen de los archivos de directivas que se van a evaluar. Si hace clic en **servidor**, puede realizar una evaluación a petición de las directivas de prácticas recomendadas que se importaron previamente en la administración basada en directivas en un servidor local o remoto. En este tutorial, hará clic en **archivos**y, a continuación, seleccionará los archivos de directivas individuales que desea evaluar. Para ello, siga estos pasos.  
  
    1.  Haga clic en **archivos**.  
  
    2.  Junto a **archivos**, haga clic en el botón de puntos suspensivos (**...**).  
  
    3.  En el cuadro de diálogo **seleccionar Directiva** , busque la carpeta siguiente, que contiene las directivas de prácticas recomendadas:  
  
         **C:\Archivos de programa (x86)\Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  La ruta de acceso puede variar según dónde instalara los archivos de programa de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , si ejecuta un sistema operativo de 32 bits o de 64 bits y el identificador de idioma.  
  
    4.  Seleccione uno o varios archivos de directivas. XML para evaluar y, a continuación, haga clic en **abrir**.  
  
         La lista de archivos seleccionados aparece en el cuadro **archivos** .  
  
    5.  En el cuadro de diálogo **Seleccionar origen** , haga clic en **Aceptar**.  
  
    6.  Si aparece el cuadro de diálogo **cargando directivas** , haga clic en **cerrar**.  
  
     Las directivas que ha seleccionado se muestran en la página **selección de directiva** . Tenga en cuenta que un icono de advertencia al lado de una directiva indica que la directiva contiene scripts.  
  
5.  Haga clic en **evaluar** para evaluar las directivas.  
  
     En la tabla de **resultados** , se enumeran los resultados de cada Directiva. Un icono con una "x" roja indica que se produjo un error en el cumplimiento de la directiva.  
  
6.  En el caso de algunos errores de las directivas, la administración basada en directivas le permite aplicar inmediatamente el cumplimiento de las directivas en el destino. Con tales errores, una casilla aparecerá al lado de la directiva que ha generado el error. Si activa la casilla, el botón **aplicar** está disponible. Al hacer clic en **aplicar**, la configuración no compatible se actualizará automáticamente en la instancia de destino.  
  
    > [!CAUTION]  
    >  Asegúrese de que entiende totalmente la configuración de las directivas antes de actualizar una instancia de destino automáticamente. Se recomienda que después de activar una o varias casillas, haga clic en **script**y elija una ubicación de salida para que pueda revisar el [!INCLUDE[tsql](../includes/tsql-md.md)] código subyacente antes de aplicar los cambios.  
  
7.  Para ver los resultados detallados de una directiva, haga clic en la Directiva en la tabla de **resultados** .  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Realizar una evaluación a petición usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
