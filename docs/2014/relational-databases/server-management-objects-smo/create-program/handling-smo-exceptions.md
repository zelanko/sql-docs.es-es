---
title: Controlar excepciones SMO | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SMO [SQL Server], exceptions
- exceptions [SMO]
- SQL Server Management Objects, exceptions
- inner exceptions [SMO]
ms.assetid: 4c725ff2-6588-44ca-b86a-87979e164153
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 595da161660b60845c02d71e22411a2a4eba009c
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807397"
---
# <a name="handling-smo-exceptions"></a>Controlar excepciones SMO
  En código administrado, se producen excepciones cuando se produce un error. Los métodos y propiedades SMO no notifican el fin correcto o incorrecto en el valor devuelto. En su lugar, las excepciones se pueden detectar y controlar mediante un controlador de excepciones.  
  
 En SMO existen diferentes clases de excepción. Se puede extraer información sobre la excepción de las propiedades de excepción como la propiedad `Message`, que proporciona un mensaje de texto sobre la excepción.  
  
 Las instrucciones de control de excepciones son específicas del lenguaje de programación. Por ejemplo, en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic es la instrucción `Catch`.  
  
## <a name="inner-exceptions"></a>Excepciones internas  
 Las excepciones pueden ser o generales o específicas. Las excepciones generales contienen un conjunto de excepciones específicas. Se pueden utilizar varias instrucciones `Catch` para controlar los errores anticipados y permitir que los errores restantes pasen explícitamente a código general de control de errores. Las excepciones se producen a menudo en una secuencia en cascada. Con frecuencia, una excepción SQL puede provocar una excepción SMO. La manera de detectar si es esto lo que ha sucedido consiste en utilizar la propiedad `InnerException` de forma consecutiva para determinar la excepción original que produjo la excepción final de nivel superior.  
  
> [!NOTE]  
>  El `SQLException` excepción está declarado en el **System.Data.SqlClient** espacio de nombres.  
  
 ![Un diagrama que muestra los niveles de la que una excepción](../../../database-engine/dev-guide/media/exception-flow.gif "un diagrama que muestra los niveles de la que una excepción")  
  
 El diagrama muestra el flujo de excepciones a través de los niveles de la aplicación.  
  
## <a name="example"></a>Ejemplo  
 Para utilizar cualquier ejemplo de código que se proporcione, deberá elegir el entorno de programación, la plantilla de programación y el lenguaje de programación con los que crear su aplicación. Para obtener más información, consulte [crear un Visual C&#35; proyecto SMO en Visual Studio .NET](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md) o [crear un proyecto de Visual Basic SMO en Visual Studio .NET](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md).  
  
## <a name="catching-an-exception-in-visual-basic"></a>Detectar una excepción en Visual Basic  
 En este ejemplo de código se muestra cómo usar la instrucción `Try...Catch...Finally` de [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] para detectar una excepción SMO. Todas las excepciones SMO tienen el tipo SmoException y se enumeran en la referencia SMO. La secuencia de excepciones internas se muestra para indicar la raíz del error. Para obtener más información, vea la documentación de [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] .NET.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBExceptions1](SMO How to#SMO_VBExceptions1)]  -->  
  
## <a name="catching-an-exception-in-visual-c"></a>Detectar una excepción en Visual C#  
 En este ejemplo de código se muestra cómo usar la instrucción `Try...Catch...Finally` de Visual C# para detectar una excepción SMO. Todas las excepciones SMO tienen el tipo SmoException y se enumeran en la referencia SMO. La secuencia de excepciones internas se muestra para indicar la raíz del error. Para obtener más información, vea la documentación de Visual C#.  
  
```  
{   
//This sample requires the Microsoft.SqlServer.Management.Smo.Agent namespace to be included.   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Define an Operator object variable by supplying the parent SQL Agent and the name arguments in the constructor.   
//Note that the Operator type requires [] parenthesis to differentiate it from a Visual Basic key word.   
op = new Operator(srv.JobServer, "Test_Operator");   
op.Create();   
//Start exception handling.   
try {   
    //Create the operator again to cause an SMO exception.   
    OperatorCategory opx;   
    opx = new OperatorCategory(srv.JobServer, "Test_Operator");   
    opx.Create();   
}   
//Catch the SMO exception   
catch (SmoException smoex) {   
    Console.WriteLine("This is an SMO Exception");   
   //Display the SMO exception message.   
   Console.WriteLine(smoex.Message);   
   //Display the sequence of non-SMO exceptions that caused the SMO exception.   
   Exception ex;   
   ex = smoex.InnerException;   
   while (!object.ReferenceEquals(ex.InnerException, (null))) {   
      Console.WriteLine(ex.InnerException.Message);   
      ex = ex.InnerException;   
    }   
    }   
   //Catch other non-SMO exceptions.   
   catch (Exception ex) {   
      Console.WriteLine("This is not an SMO exception.");   
}   
}  
```  
  
  
