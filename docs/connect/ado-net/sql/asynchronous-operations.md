---
title: Operaciones asincrónicas
description: Describe cómo realizar operaciones asincrónicas de base de datos mediante una API modelada según el modelo asincrónico usado por .NET Framework.
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 79cde936328476408fabb3df7a6bff8d983ace1c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452324"
---
# <a name="asynchronous-operations"></a>Operaciones asincrónicas

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Algunas operaciones de base de datos, como las ejecuciones de comandos, pueden tardar mucho tiempo en completarse. En tal caso, las aplicaciones de un único subproceso deben bloquear otras operaciones y esperar a que el comando finalice para poder continuar sus propias operaciones. En cambio, el poder asignar la operación de ejecución prolongada a un subproceso en segundo plano permite que el subproceso en primer plano permanezca activo durante toda la operación. En una aplicación de Windows, por ejemplo, la delegación de la operación de ejecución prolongada en un subproceso en segundo plano permite que el subproceso de la interfaz de usuario siga respondiendo mientras se ejecuta la operación.  
  
.NET proporciona varios patrones de diseño asincrónicos estándar que los desarrolladores pueden usar para aprovechar los subprocesos en segundo plano y liberar la interfaz de usuario o los subprocesos de alta prioridad para realizar otras operaciones en su clase <xref:Microsoft.Data.SqlClient.SqlCommand>. En concreto, los métodos <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> y <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>, emparejados con los métodos <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> y <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A>, proporcionan la compatibilidad asincrónica.  
  
> [!NOTE]
>  La programación asincrónica es una característica principal de .NET. Para obtener más información sobre las diferentes técnicas asincrónicas disponibles para los desarrolladores, consulte [llamar a métodos sincrónicos de forma asincrónica](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously).  
  
Aunque el uso de técnicas asincrónicas con características de ADO.NET no agrega ninguna consideración especial, es importante tener en cuenta las ventajas e inconvenientes de la creación de aplicaciones multiproceso. En los ejemplos siguientes de esta sección se indican varios problemas importantes que los desarrolladores deben tener en cuenta al crear aplicaciones que incorporan funcionalidad multiproceso.  
  
## <a name="in-this-section"></a>En esta sección  
[Aplicaciones Windows que usan devoluciones de llamada](windows-applications-callbacks.md)  
Proporciona un ejemplo en el que se muestra cómo ejecutar un comando asincrónico de forma segura, controlando correctamente la interacción con un formulario y su contenido desde un subproceso independiente.  
  
[Aplicaciones ASP.NET que usan identificadores de espera](aspnet-apps-use-wait-handles.md)  
Proporciona un ejemplo en el que se muestra cómo ejecutar varios comandos simultáneos desde una página de ASP.NET, mediante el uso de identificadores de espera para administrar la operación cuando se completan todos los comandos.  
  
[Sondeo de aplicaciones de consola](poll-console-applications.md)  
Proporciona un ejemplo que muestra el uso del sondeo para esperar a que se complete la ejecución de un comando asincrónico desde una aplicación de consola. Esta técnica también es válida en una biblioteca de clases u otra aplicación sin una interfaz de usuario.  
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)
- [Llamar a métodos sincrónicos de forma asincrónica](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
