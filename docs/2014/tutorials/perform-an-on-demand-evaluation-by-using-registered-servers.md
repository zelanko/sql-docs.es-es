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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66822376"
---
# <a name="perform-an-on-demand-evaluation-by-using-registered-servers"></a>Realizar una evaluación a petición usando servidores registrados

  Puede realizar una evaluación a petición de las directivas de prácticas recomendadas con una o más instancias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utilizando servidores registrados. Puede utilizar grupos de servidores locales o un servidor de administración central.  
  
> [!NOTE]  
>  Puede realizar una evaluación a petición de las directivas de prácticas recomendadas con los miembros del grupo de servidores que ejecutan [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] o una versión posterior de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Sin embargo, puede recibir un error de excepción si hay algunas propiedades a las que se haga referencia en una directiva que no se admita en [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] o [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)].  
  
## <a name="prerequisites"></a>Requisitos previos  
 Para realizar esta tarea, debe haber configurado uno o más registros de servidor en los servidores registrados. Para obtener más información, vea los temas siguientes:  
  
-   [Crear o editar un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
-   [Registra un servidor conectado &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
-   [Crear un servidor de administración central y un grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-evaluate-best-practices-policies-against-a-server-group"></a>Para evaluar las directivas de prácticas recomendadas con un grupo de servidores  
  
1.  En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], en el menú **Ver** , haga clic en **Servidores registrados**.  
  
2.  Expanda **motor de base de datos**y, a continuación, expanda **grupos**de servidores locales o **servidores de administración central**, en función de la configuración.  
  
3.  Realice cualquiera de las siguientes acciones:  
  
    -   Para evaluar las directivas en todos los servidores administrados por el grupo de servidores local o el servidor de administración central, haga clic con el botón secundario en el nombre del grupo de servidores local o en el nombre del servidor de administración central y, a continuación, haga clic en **evaluar directivas**.  
  
        > [!NOTE]  
        >  Al evaluar las directivas a través de un servidor de administración central, no se evalúan con el propio servidor de administración central.  
  
    -   Para evaluar las directivas con respecto a un servidor o grupo de servidores específico, expanda **grupos de servidores locales** o el nombre del servidor de administración central, haga clic con el botón secundario en el servidor o grupo de servidores del que desee evaluar las directivas y, a continuación, haga clic en **evaluar directivas**.  
  
4.  En el cuadro de diálogo **evaluar directivas** , junto al cuadro **origen** , haga clic en el botón de puntos suspensivos (**...**).  
  
5.  En el cuadro de diálogo **Seleccionar origen** , puede seleccionar **archivos** o **servidor** como origen de los archivos de directivas que se van a evaluar. Si hace clic en **servidor**, puede realizar una evaluación a petición de las directivas de prácticas recomendadas que se importaron previamente en la administración basada en directivas en un servidor local o remoto. En este tutorial, hará clic en **archivos**y, a continuación, seleccionará los archivos de directivas individuales que desea evaluar. Para ello, realice los pasos siguientes:  
  
    1.  Haga clic en **archivos**.  
  
    2.  Junto a **archivos**, haga clic en el botón de puntos suspensivos (**...**).  
  
    3.  Seleccione uno o varios archivos de directivas. XML para evaluar y, a continuación, haga clic en **abrir**.  
  
         La lista de archivos seleccionados aparece en el cuadro **archivos** .  
  
    4.  En el cuadro de diálogo **Seleccionar origen** , haga clic en **Aceptar**.  
  
    5.  Si aparece el cuadro de diálogo **cargando directivas** , haga clic en **cerrar**.  
  
     Las directivas que ha seleccionado se muestran en la página **selección de directiva** . Tenga en cuenta que un icono de advertencia al lado de una directiva indica que la directiva contiene scripts.  
  
6.  Haga clic en **evaluar** para evaluar las directivas.  
  
7.  En el caso de algunos errores de las directivas, la administración basada en directivas le permite aplicar inmediatamente el cumplimiento de las directivas en el destino. Con tales errores, una casilla aparecerá al lado de la directiva que ha generado el error. Si activa la casilla o hace clic en la fila que contiene la Directiva con errores, las casillas aparecen en el panel **detalles de destino** junto a las instancias de destino que no pudieron realizar la evaluación. Si se selecciona cualquiera de las casillas, el botón **aplicar** está disponible. Al hacer clic en **aplicar**, la configuración no compatible se actualizará automáticamente en las instancias de destino seleccionadas.  
  
    > [!CAUTION]  
    >  Asegúrese de que entiende totalmente la configuración de las directivas antes de actualizar una instancia de destino automáticamente. Se recomienda que después de activar una o varias casillas, haga clic en **script**y elija una ubicación de salida para que pueda revisar el [!INCLUDE[tsql](../includes/tsql-md.md)] código subyacente antes de aplicar los cambios.  
  
8.  Para ver los resultados detallados de una directiva, haga clic en la Directiva en la tabla de **resultados** . En la tabla **detalles del destino** se muestran los detalles de cada instancia.  
  
## <a name="next-lesson"></a>Lección siguiente  
 [Lección 2: Evaluación de las directivas de procedimientos recomendados de forma programada](../../2014/tutorials/lesson-2-evaluate-best-practices-policies-on-a-scheduled-basis.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar y aplicar las prácticas recomendadas mediante la administración basada en directivas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)   
 [Administrar varios servidores mediante Servidores de administración central](../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
