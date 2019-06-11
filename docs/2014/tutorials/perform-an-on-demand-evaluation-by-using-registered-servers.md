---
title: Realizar una evaluación a petición mediante el uso de servidores registrados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: c14034ef-6e0b-4df5-8072-bfb8d90b3172
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a3a79a6ec655e91264d6fcc00db5a920ad82a21e
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822376"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>Realizar una evaluación a petición usando servidores registrados

  Puede realizar una evaluación a petición de las directivas de prácticas recomendadas con una o más instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizando servidores registrados. Puede utilizar grupos de servidores locales o un servidor de administración central.  
  
> [!NOTE]  
>  Puede realizar una evaluación a petición de las directivas de prácticas recomendadas con los miembros del grupo de servidores que ejecutan [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] o una versión posterior de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sin embargo, puede recibir un error de excepción si hay algunas propiedades a las que se haga referencia en una directiva que no se admita en [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] o [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)].  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar esta tarea, debe haber configurado uno o más registros de servidor en los servidores registrados. Para obtener más información, vea los temas siguientes:  
  
-   [Crear o editar un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [Registrar un servidor conectado &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
-   [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>Para evaluar las directivas de prácticas recomendadas con un grupo de servidores  
  
1.  En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], en el menú **Ver** , haga clic en **Servidores registrados**.  
  
2.  Expanda **motor de base de datos**y, a continuación, expanda **grupos de servidores locales**, o **servidores de Administración Central**, según la configuración.  
  
3.  Realice una de las acciones siguientes:  
  
    -   Para evaluar las directivas con todos los servidores que están administrados por el grupo de servidores locales o el servidor de administración central, haga clic en el nombre del grupo de servidor local o el nombre del servidor de administración central y, a continuación, haga clic en **evaluar directivas** .  
  
        > [!NOTE]  
        >  Al evaluar las directivas a través de un servidor de administración central, no se evalúan con el propio servidor de administración central.  
  
    -   Para evaluar las directivas con un servidor específico o un grupo de servidores, expanda **grupos de servidores locales** o asigne un nombre, haga clic en el servidor o grupo de servidores que desea evaluar directivas con y, a continuación, haga clic en el servidor de administración central **Evaluar directivas**.  
  
4.  En el **evaluar directivas** cuadro de diálogo, junto a la **origen** cuadro, haga clic en el botón de puntos suspensivos ( **...** ) botón.  
  
5.  En el **Seleccionar origen** cuadro de diálogo, puede seleccionar cualquiera **archivos** o **Server** como origen de los archivos de directivas para evaluar. Si hace clic en **Server**, puede realizar una evaluación a petición de las directivas de prácticas recomendadas que se importaron previamente en la administración basada en directivas en un servidor local o remoto. En este tutorial, hará clic en **archivos**y, a continuación, seleccione los archivos de directiva individuales que se va a evaluar. Para ello, siga estos pasos:  
  
    1.  Haga clic en **archivos**.  
  
    2.  Junto a **archivos**, haga clic en el botón de puntos suspensivos ( **...** ) botón.  
  
    3.  Seleccione uno o varios archivos de directiva .xml para evaluar y, a continuación, haga clic en **abierto**.  
  
         La lista de archivos seleccionados aparece en el **archivos** cuadro.  
  
    4.  En el **Seleccionar origen** cuadro de diálogo, haga clic en **Aceptar**.  
  
    5.  Si el **cargando directivas** aparece el cuadro de diálogo, haga clic en **cerrar**.  
  
     Las directivas que seleccionó se muestran en el **selección de directiva** página. Tenga en cuenta que un icono de advertencia al lado de una directiva indica que la directiva contiene scripts.  
  
6.  Haga clic en **Evaluate** para evaluar las directivas.  
  
7.  En el caso de algunos errores de las directivas, la administración basada en directivas le permite aplicar inmediatamente el cumplimiento de las directivas en el destino. Con tales errores, una casilla aparecerá al lado de la directiva que ha generado el error. Si selecciona la casilla de verificación, o haga clic en la fila con la directiva con errores, las casillas de verificación aparecen en la **detalles del destino** panel junto a las instancias de destino que ha fallado la evaluación. Si se ha seleccionado alguna de las casillas de verificación, la **aplicar** botón esté disponible. Al hacer clic en **aplicar**, la configuración incompatible se actualizará automáticamente en las instancias de destino que ha seleccionado.  
  
    > [!CAUTION]  
    >  Asegúrese de que entiende totalmente la configuración de las directivas antes de actualizar una instancia de destino automáticamente. Se recomienda que después de seleccionar una o varias casillas de verificación, hacer clic en **Script**y elija una ubicación de salida para que pueda revisar subyacente [!INCLUDE[tsql](../includes/tsql-md.md)] antes de aplicar los cambios de código.  
  
8.  Para ver los resultados detallados de una directiva, haga clic en la directiva en el **resultados** tabla. El **detalles del destino** tabla muestra los detalles para cada instancia.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Evaluar las directivas de prácticas recomendadas de forma programada](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>Vea también  
 [Supervisar y aplicar las prácticas recomendadas usando administración basada en directivas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [Administrar varios servidores mediante Servidores de administración central](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
