---
title: Definir dimensiones vinculadas | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: d5ad5eae-5dde-46a6-91c3-c8766d016dec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 409cdbaa10dc93c5cb659961f084d76bc3370bde
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726479"
---
# <a name="define-linked-dimensions"></a>Definir dimensiones vinculadas
  Una dimensión vinculada se basa en una dimensión creada y almacenada en otra base de datos de Analysis Services de la misma versión y con el mismo nivel de compatibilidad. Con una dimensión vinculada, puede crear, almacenar y mantener una dimensión en una base de datos y permitir que esa dimensión esté disponible para los usuarios de varias bases de datos. Para los usuarios, una dimensión vinculada es como cualquier otra dimensión.  
  
 Las dimensiones vinculadas son de solo lectura. Si desea modificar la dimensión o crear relaciones nuevas, debe cambiar la dimensión de origen, y después eliminar y volver a crear la dimensión vinculada y sus relaciones. No puede actualizar una dimensión vinculada para elegir cambios del objeto de origen.  
  
 Todas las dimensiones y grupos de medida relacionados deben proceder de la misma base de datos de origen. No puede crear relaciones entre los grupos de medida locales y las dimensiones vinculadas que se agreguen al cubo. Una vez que las dimensiones vinculadas y los grupos de medida se han agregado al cubo local, las relaciones entre ellos deben mantenerse en la base de datos de origen.  
  
> [!NOTE]  
>  Como la actualización no está disponible, la mayoría de los desarrolladores de Analysis Services copian dimensiones en lugar de vincularlas. Puede copiar dimensiones entre proyectos dentro de la misma solución. Para obtener más información, vea [Actualizar una dimensión vinculada en SSAS](http://sqlblog.com/blogs/marco_russo/archive/2006/09/12/refresh-of-a-linked-dimension-in-ssas.aspx).  
  
## <a name="prerequisites"></a>Requisitos previos  
 La base de datos de origen que proporciona la dimensión y la base de datos actual que la usa deben tener la misma versión y el mismo nivel de compatibilidad. Para obtener más información, consulte [establecer el nivel de compatibilidad de una base de datos multidimensionales &#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
 La base de datos de origen debe estar implementada y en línea. Los servidores que publican o usan objetos vinculados deben configurarse para permitir la operación (vea la información que se incluye a continuación).  
  
 La dimensión que pretende usar no puede ser una dimensión vinculada.  
  
## <a name="configure-server-to-allow-linked-objects"></a>Configurar el servidor para permitir objetos vinculados  
  
1.  En SQL Server Management Studio, conéctese a un servidor de Analysis Services. En el Explorador de objetos, haga clic con el botón derecho en el nombre del servidor y, después, seleccione **Facetas**.  
  
2.  Establezca **LinkedObjectsLinksFromOtherInstancesEnabled** en **True** para permitir que el servidor emita solicitudes de los objetos vinculados que residen en las bases de datos que se ejecutan en otras instancias.  
  
3.  Establezca **LinkedObjectsLinksToOtherInstances** en **True** para que el servidor solicite datos de objetos vinculados de las bases de datos que se ejecutan en otras instancias.  
  
## <a name="create-a-linked-dimension-in-sql-server-data-tools"></a>Cree una dimensión vinculada en Herramientas de datos de SQL Server  
  
1.  Inicie el asistente. En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic con el botón derecho en la carpeta **Dimensiones** de una base de datos o proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, después, haga clic en **Nueva dimensión vinculada**.  
  
2.  Conéctese a la base de datos de Analysis Services que proporciona la dimensión. En la página **Seleccionar un origen de datos** del Asistente para objetos vinculados, elija el origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o cree uno nuevo.  
  
3.  En la página **Seleccionar objetos** del asistente, elija las dimensiones a las que desee vincularse en la base de datos remota.  
  
4.  En la página **Finalización del asistente** , puede obtener una vista previa de los objetos vinculados. Si vincula una dimensión que tenga el mismo nombre que una que ya existe, se anexa un número ordinal al nombre (empezando con '1' para el primer nombre duplicado). Al completar el asistente, la dimensión se agrega a la carpeta **Dimensiones** .  
  
##  <a name="bkmk_CreateNew"></a> Crear una nueva conexión de origen de datos con una base de datos de Analysis Services  
 Use el Asistente para nuevos orígenes de datos para agregar a la conexión del proyecto información sobre la base de datos de Analysis Services que proporciona la dimensión. Puede iniciar el asistente haciendo clic en **Nuevo origen de datos** en la página Seleccionar un origen de datos del Asistente para objetos vinculados.  
  
1.  En el Asistente para orígenes de datos, en la página Seleccionar cómo definir la conexión, haga clic en **Nuevo**.  
  
2.  En el Administrador de conexiones, compruebe que el proveedor está establecido en **Proveedor OLE DB de Microsoft\OLE DB nativo para Analysis Services 11.0**.  
  
3.  Escriba el nombre del servidor (use *servername*\\*nombreDeInstancia* para una instancia con nombre)<sup>1</sup> o tipo **localhost** a conectarse a un servidor de Analysis Services que se está ejecutando en el mismo equipo.  
  
4.  Use la autenticación de Windows para la conexión.  
  
5.  En **Catálogo inicial**, haga clic en la flecha hacia abajo para seleccionar una base de datos de este servidor.  
  
6.  En el Asistente para orígenes de datos, haga clic en **Siguiente** para continuar.  
  
7.  En la página Información de suplantación, haga clic en **Utilizar la cuenta de servicio**. Haga clic en **Siguiente**y, a continuación, finalice el Asistente. La conexión que acaba de definir se seleccionará en el Asistente para objetos vinculados.  
  
## <a name="next-steps"></a>Pasos siguientes  
 No puede cambiar la estructura de una dimensión vinculada, de manera que no se la puede ver en la pestaña **Estructura de dimensión** del Diseñador de dimensiones. Después de procesar la dimensión vinculada, puede verla en la pestaña **Explorador** . También puede cambiar su nombre y crear una traducción del nombre.  
  
## <a name="see-also"></a>Vea también  
 [Establecer la compatibilidad de nivel de base de datos Multidimensional &#40;Analysis Services&#41;](compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Grupos de medida vinculados](linked-measure-groups.md)   
 [Relaciones de dimensión](../multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
  
  
