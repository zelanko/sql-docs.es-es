---
title: Adjuntar y separar bases de datos de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.ssms.detachdatabase.f1
- sql12.asvs.ssms.attachdatabase.f1
- sql12.asvs.ssmsimbi.AttachDatabase.f1
- sql12.asvs.ssmsimbi.DetachDatabase.f1
helpviewer_keywords:
- databases [Analysis Services], attach
- databases [Analysis Services], detach
ms.assetid: 41887413-2d47-49b8-8614-553cb799fb18
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c73417ea9d74588c55177527abdbb42a33c4496e
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50144920"
---
# <a name="attach-and-detach-analysis-services-databases"></a>Adjuntar y separar bases de datos de Analysis Services
  Con frecuencia se producen situaciones en las que un administrador de bases de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quiere dejar sin conexión una base de datos durante un tiempo para después volver a ponerla en línea en la misma instancia de servidor o en otra distinta. Estas situaciones suelen responder a necesidades empresariales, como mover la base de datos a otro disco para mejorar el rendimiento, disponer de más espacio para que la base de datos pueda crecer o actualizar un producto. Para todos estos y otros casos, el `Attach` y `Detach` comandos permiten la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dba para desconectar la base de datos y ponerla a conectarla con poco esfuerzo.  
  
## <a name="attach-and-detach-commands"></a>Los comandos Attach y Detach  
 El comando `Attach` le permite poner en línea una base de datos que se dejó sin conexión. Puede adjuntar la base de datos a la instancia del servidor original o a otra instancia. Al adjuntar una base de datos, es posible especificar el valor de la propiedad **ReadWriteMode** de la base de datos. El comando `Detach` le permite dejar sin conexión una base de datos del servidor.  
  
## <a name="attach-and-detach-usage"></a>Uso de Attach y Detach  
 El comando `Attach` se utiliza para poner en línea una estructura de base de datos existente. Si la base de datos se adjunta en el modo `ReadWrite`, solo puede adjuntarse una vez a una instancia de servidor. Sin embargo, si la base de datos se adjunta en el modo `ReadOnly`, puede adjuntarse varias veces a distintas instancias de servidor. No obstante, la misma base de datos no puede adjuntarse más de una vez a la misma instancia de servidor. Se produce un error cuando se intenta adjuntar la misma base de datos más de una vez, incluso si los datos se han copiado en carpetas distintas.  
  
> [!IMPORTANT]  
>  Si se necesitó una contraseña para separar la base de datos, deberá usarse la misma contraseña para adjuntarla.  
  
 El comando `Detach` se utiliza para dejar sin conexión una estructura de base de datos existente. Cuando separe una base de datos, conviene que proporcione una contraseña para proteger los metadatos confidenciales.  
  
> [!IMPORTANT]  
>  Para proteger el contenido de los archivos de datos, debería utilizar una lista de control de acceso para la carpeta, las subcarpetas y los archivos de datos.  
  
 Cuando se separa una base de datos, el servidor sigue estos pasos.  
  
|Separar una base de datos de lectura/escritura|Separar una base de datos de solo lectura|  
|--------------------------------------|-------------------------------------|  
|1) El servidor emite una solicitud de bloqueo CommitExclusive para la base de datos<br />2) El servidor espera hasta que todas las transacciones en curso se confirmen o se reviertan<br />3) El servidor genera todos los metadatos que necesita para separar la base de datos<br />4) La base de datos se marca como eliminada<br />5) El servidor confirma la transacción|1) La base de datos se marca como eliminada<br />2) El servidor confirma la transacción<br /><br /> <br /><br /> Nota: No es posible cambiar la contraseña de separación para una base de datos de solo lectura. Se produce un error si se proporciona el parámetro de contraseña para una base de datos adjuntada que ya contiene una contraseña.|  
  
 Los comandos `Attach` y `Detach` se deben ejecutar como operaciones únicas. No se pueden combinar con otras operaciones en la misma transacción. Además, el `Attach` y `Detach` comandos son comandos transaccionales atómicos. Esto significa que la operación se realizará correctamente o producirá un error. No se dejará ninguna base de datos en un estado incompleto.  
  
> [!IMPORTANT]  
>  Se necesitan privilegios de administrador de bases de datos o de servidores para ejecutar el comando `Detach`.  
  
> [!IMPORTANT]  
>  Se necesitan privilegios de administrador de servidores para ejecutar el comando `Attach`.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Mover una base de datos de Analysis Services](move-an-analysis-services-database.md)   
 [Modos de la propiedad de base de datos ReadWriteMode](database-readwritemodes.md)   
 [Cambiar entre los modos ReadOnly y ReadWrite en una base de datos de Analysis Services](switch-an-analysis-services-database-between-readonly-and-readwrite-modes.md)   
 [Elemento Detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)  
  
  
