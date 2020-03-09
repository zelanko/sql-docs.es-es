---
title: Operaciones asincrónicas
description: Describe cómo realizar operaciones asincrónicas de base de datos mediante una API modelada según el modelo asincrónico usado por .NET Framework.
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: bc2a921e3aec0068c11b2baab45c396d853a1a36
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2020
ms.locfileid: "78897061"
---
# <a name="asynchronous-operations"></a>Operaciones asincrónicas

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Algunas operaciones de base de datos, como las ejecuciones de comandos, pueden tardar mucho tiempo en completarse. En estos casos, las aplicaciones con un único subproceso deben bloquear otras operaciones y esperar hasta que el comando finaliza antes de continuar con otras operaciones. En cambio, el poder asignar la operación de ejecución prolongada a un subproceso en segundo plano permite que el subproceso en primer plano permanezca activo durante toda la operación. En una aplicación Windows, por ejemplo, delegar la operación de larga duración a un subproceso en segundo plano permite que el subproceso de la interfaz de usuario siga respondiendo.  
  
.NET proporciona varios patrones de diseño asincrónicos estándar que los desarrolladores pueden usar para aprovechar los subprocesos en segundo plano y liberar la interfaz de usuario o los subprocesos de alta prioridad para realizar otras operaciones en su clase <xref:Microsoft.Data.SqlClient.SqlCommand>. En concreto, los métodos <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> y <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>, emparejados con los métodos <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> y <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A>, proporcionan la compatibilidad asincrónica.  
  
> [!NOTE]
>  La programación asincrónica es una característica principal de .NET. Para obtener más información sobre las diferentes técnicas asincrónicas disponibles para los desarrolladores, vea el artículo sobre cómo [llamar a métodos sincrónicos de forma asincrónica](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously).  
  
Aunque el uso de técnicas asincrónicas con características de ADO.NET no agrega ninguna consideración especial, es importante tener en cuenta las ventajas e inconvenientes de la creación de aplicaciones multiproceso. En los ejemplos siguientes de esta sección se indican varios problemas importantes que los desarrolladores deben tener en cuenta al crear aplicaciones que incorporan funcionalidades multiproceso.  
  
## <a name="in-this-section"></a>En esta sección  
[Aplicaciones Windows que usan devoluciones de llamada](windows-applications-callbacks.md)  
Proporciona un ejemplo en el que se muestra cómo ejecutar un comando asincrónico de forma segura, controlando correctamente la interacción con un formulario y su contenido desde un subproceso independiente.  
  
[Aplicaciones ASP.NET que usan identificadores de espera](aspnet-apps-use-wait-handles.md)  
Proporciona un ejemplo en el que se muestra cómo ejecutar varios comandos simultáneos desde una página ASP.NET. Para ello, se usan identificadores Wait para administrar la operación cuando se completan todos los comandos.  
  
[Sondeo de aplicaciones de consola](poll-console-applications.md)  
Proporciona un ejemplo que muestra el uso del sondeo para esperar a que se complete la ejecución de un comando asincrónico desde una aplicación de consola. Esta técnica también es válida en una biblioteca de clases u otra aplicación sin una interfaz de usuario.  
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)
- [Llamar a métodos sincrónicos de forma asincrónica](https://docs.microsoft.com/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
