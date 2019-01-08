---
title: Realizar una evaluación a petición mediante el Explorador de objetos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ee6d3b79-18bc-49d3-8a1d-0c0905b990f0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: ddb0eeb783f2bdb617ba5c2ac2b18896c23abdcc
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52536562"
---
# <a name="perform-an-on-demand-evaluation-by-using-object-explorer"></a>Realizar una evaluación a petición usando Explorador de objetos
  En esta tarea, utilizará el Explorador de objetos para realizar una evaluación a petición de las directivas de prácticas recomendadas para [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] en una instancia única de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  También puede evaluar las directivas en una instancia única a través de servidores registrados. Para obtener más información, consulte [realizar una evaluación a petición mediante el uso de servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
## <a name="prerequisites"></a>Requisitos previos  
 Esta lección se basa en la versión de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
> [!NOTE]  
>  Para realizar una evaluación de directivas de prácticas recomendadas con instancias que se ejecutan a petición [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], use el procedimiento del tema [realizar una evaluación a petición mediante el uso de servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md).  
  
### <a name="to-perform-an-on-demand-evaluation-by-using-object-explorer"></a>Realizar una evaluación a petición usando Explorador de objetos  
  
1.  Inicie [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]y después conéctese a [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
2.  En el Explorador de objetos, expanda **administración**, expanda **administración de directivas**, haga clic en **directivas**y, a continuación, haga clic en **Evaluate**.  
  
    > [!NOTE]  
    >  De forma predeterminada, la instancia local se utiliza como el origen de las directivas. Si ha importado las directivas de prácticas recomendadas previamente, se enumerarán junto con cualquier otra directiva que haya creado. Puede seleccionar cualquiera de las directivas de prácticas recomendadas importadas y, a continuación, haga clic en **Evaluate**. Si no ha importado las directivas de prácticas recomendadas, continúe con este procedimiento.  
  
3.  En el **evaluar directivas** cuadro de diálogo, junto a la **origen** cuadro, haga clic en el botón de puntos suspensivos (**...** ) botón.  
  
4.  En el **Seleccionar origen** cuadro de diálogo, puede seleccionar cualquiera **archivos** o **Server** como origen de los archivos de directivas para evaluar. Si hace clic en **Server**, puede realizar una evaluación a petición de las directivas de prácticas recomendadas que se importaron previamente en la administración basada en directivas en un servidor local o remoto. En este tutorial, hará clic en **archivos**y, a continuación, seleccione los archivos de directiva individuales que se va a evaluar. Para ello, siga estos pasos:  
  
    1.  Haga clic en **archivos**.  
  
    2.  Junto a **archivos**, haga clic en el botón de puntos suspensivos (**...** ) botón.  
  
    3.  En el **Seleccionar directiva** cuadro de diálogo, vaya a la carpeta siguiente, que contiene las directivas de prácticas recomendadas:  
  
         **C:\Program archivos (x86) \Microsoft SQL Server\110\Tools\Policies\DatabaseEngine\1033**  
  
        > [!NOTE]  
        >  La ruta de acceso puede variar según dónde instalara los archivos de programa de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , si ejecuta un sistema operativo de 32 bits o de 64 bits y el identificador de idioma.  
  
    4.  Seleccione uno o varios archivos de directiva .xml para evaluar y, a continuación, haga clic en **abierto**.  
  
         La lista de archivos seleccionados aparece en el **archivos** cuadro.  
  
    5.  En el **Seleccionar origen** cuadro de diálogo, haga clic en **Aceptar**.  
  
    6.  Si el **cargando directivas** aparece el cuadro de diálogo, haga clic en **cerrar**.  
  
     Las directivas que seleccionó se muestran en el **selección de directiva** página. Tenga en cuenta que un icono de advertencia al lado de una directiva indica que la directiva contiene scripts.  
  
5.  Haga clic en **Evaluate** para evaluar las directivas.  
  
     En el **resultados** tabla, los resultados de cada directiva se enumeran. Un icono con una "x" roja indica que se produjo un error en el cumplimiento de la directiva.  
  
6.  En el caso de algunos errores de las directivas, la administración basada en directivas le permite aplicar inmediatamente el cumplimiento de las directivas en el destino. Con tales errores, una casilla aparecerá al lado de la directiva que ha generado el error. Si selecciona la casilla de verificación, la **aplicar** botón esté disponible. Al hacer clic en **aplicar**, la configuración incompatible se actualizará automáticamente en la instancia de destino.  
  
    > [!CAUTION]  
    >  Asegúrese de que entiende totalmente la configuración de las directivas antes de actualizar una instancia de destino automáticamente. Se recomienda que después de seleccionar una o varias casillas de verificación, hacer clic en **Script**y elija una ubicación de salida para que pueda revisar subyacente [!INCLUDE[tsql](../includes/tsql-md.md)] antes de aplicar los cambios de código.  
  
7.  Para ver los resultados detallados de una directiva, haga clic en la directiva en el **resultados** tabla.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Realizar una evaluación a petición usando servidores registrados](../../2014/tutorials/perform-an-on-demand-evaluation-by-using-registered-servers.md)  
  
  
