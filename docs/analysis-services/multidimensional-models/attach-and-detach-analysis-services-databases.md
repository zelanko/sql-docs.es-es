---
title: Adjuntar y separar bases de datos de Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.ssmsimbi.AttachDatabase.f1
- sql13.asvs.ssms.attachdatabase.f1
- sql13.asvs.ssmsimbi.DetachDatabase.f1
- sql13.asvs.ssms.detachdatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4abef02a67a334486b123a2ed29b8119e7a29f8b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2018
---
# <a name="attach-and-detach-analysis-services-databases"></a>Adjuntar y separar bases de datos de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Con frecuencia se producen situaciones en las que un administrador de bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quiere dejar sin conexión una base de datos durante un tiempo para después volver a ponerla en línea en la misma instancia de servidor o en otra distinta. Estas situaciones suelen responder a necesidades empresariales, como mover la base de datos a otro disco para mejorar el rendimiento, disponer de más espacio para que la base de datos pueda crecer o actualizar un producto. Para estos y otros casos, los comandos **Attach** y **Detach** permiten al administrador de bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dejar sin conexión la base de datos y volver a ponerla en línea con el mínimo esfuerzo.  
  
## <a name="attach-and-detach-commands"></a>Los comandos Attach y Detach  
 El comando **Attach** le permite poner en línea una base de datos que se dejó sin conexión. Puede adjuntar la base de datos a la instancia del servidor original o a otra instancia. Al adjuntar una base de datos, es posible especificar el valor de la propiedad **ReadWriteMode** de la base de datos. El comando **Detach** le permite dejar sin conexión una base de datos del servidor.  
  
## <a name="attach-and-detach-usage"></a>Uso de Attach y Detach  
 El comando **Attach** se utiliza para poner en línea una estructura de base de datos existente. Si la base de datos se adjunta en el modo **ReadWrite** , solo puede adjuntarse una vez a una instancia de servidor. Sin embargo, si la base de datos se adjunta en el modo **ReadOnly** , puede adjuntarse varias veces a distintas instancias de servidor. No obstante, la misma base de datos no puede adjuntarse más de una vez a la misma instancia de servidor. Se produce un error cuando se intenta adjuntar la misma base de datos más de una vez, incluso si los datos se han copiado en carpetas distintas.  
  
> [!IMPORTANT]  
>  Si se necesitó una contraseña para separar la base de datos, deberá usarse la misma contraseña para adjuntarla.  
  
 El comando **Detach** se utiliza para dejar sin conexión una estructura de base de datos existente. Cuando separe una base de datos, conviene que proporcione una contraseña para proteger los metadatos confidenciales.  
  
> [!IMPORTANT]  
>  Para proteger el contenido de los archivos de datos, debería utilizar una lista de control de acceso para la carpeta, las subcarpetas y los archivos de datos.  
  
 Cuando se separa una base de datos, el servidor sigue estos pasos.  
  
|Separar una base de datos de lectura/escritura|Separar una base de datos de solo lectura|  
|--------------------------------------|-------------------------------------|  
|1) El servidor emite una solicitud de bloqueo CommitExclusive para la base de datos<br /><br /> 2) El servidor espera hasta que todas las transacciones en curso se confirmen o se reviertan<br /><br /> 3) El servidor genera todos los metadatos que necesita para separar la base de datos<br /><br /> 4) La base de datos se marca como eliminada<br /><br /> 5) El servidor confirma la transacción|1) La base de datos se marca como eliminada<br /><br /> 2) El servidor confirma la transacción<br /><br /> Nota: No es posible cambiar la contraseña de separación para una base de datos de solo lectura. Se produce un error si se proporciona el parámetro de contraseña para una base de datos adjuntada que ya contiene una contraseña.|  
  
 Los comandos **Attach** y **Detach** se deben ejecutar como operaciones únicas. No se pueden combinar con otras operaciones en la misma transacción. Por otra parte, los comandos **Attach** y **Detach** son comandos transaccionales atómicos. Esto significa que la operación se realizará correctamente o producirá un error. No se dejará ninguna base de datos en un estado incompleto.  
  
> [!IMPORTANT]  
>  Se necesitan privilegios de administrador de bases de datos o de servidores para ejecutar el comando **Detach** .  
  
> [!IMPORTANT]  
>  Se necesitan privilegios de administrador de servidores para ejecutar el comando **Attach** .  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Mover una base de datos de Analysis Services](../../analysis-services/multidimensional-models/move-an-analysis-services-database.md)   
 [ReadWriteModes de base de datos](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite](../../analysis-services/multidimensional-models/switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [Elemento Detach](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Elemento Attach](../../analysis-services/xmla/xml-elements-commands/attach-element.md)  
  
  
