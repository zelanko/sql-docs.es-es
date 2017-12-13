---
title: Control de errores en la API de TOM (Analysis Services AMO-TOM) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ec44daa0-a90e-42ad-b70d-6a7a7a4e4b7b
caps.latest.revision: "4"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5ba78401880831916adb608cb55f0c93579f84e2
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="handling-errors-in-the-tom-api-analysis-services-amo-tom"></a>Control de errores en la API de TOM (Analysis Services AMO-TOM)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Una práctica común para las bibliotecas administradas del modelo de objeto Tabular (TOM) como objetos de administración de servicios de análisis (AMO) consiste en usar excepciones como un mecanismo para informar sobre las condiciones de error al usuario.  

Cuando se detecta un error en AMO TOM, además de producir algunas excepciones de .NET estándares como puede ser **ArgumentException** y **InvalidOperationException**, TOM también puede producir varias excepciones de TOM específica.  

Se derivan de las excepciones de TOM [clase AmoException](http://msdn.microsoft.com/library/microsoft.analysisservices.amoexception.aspx), que abarcan ambas excepciones específicas TOM y AMO. 

Para ilustrar el control de excepciones en TOM, revisemos una de las excepciones más comunes, que es [OperationException clase](http://msdn.microsoft.com/library/microsoft.analysisservices.operationexception.aspx).

**OperationException** se produce cuando un usuario inicia una operación en el servidor de Analysis Services y el servidor no puede realizar una operación, ya sea porque la acción no era válida o debido a otro error interno o externo. 

Cuando se inicia, ** OperationException ** objeto contendrá una lista de errores XMLA devuelto por el servidor. 

Tenga en cuenta que el servidor no aceptará cambios que no son válidos. Si esto ocurre, revertir la **modelo** árbol en el último estado bueno conocido utilizando la [UndoLocalChanges método](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.model.undolocalchanges.aspx), corrija el modelo y volver a enviar. 

## <a name="code-example-handle-exceptions"></a>Ejemplo de código: controlar excepciones 
 
```
 try 
 { 
  // Change the Model, for example create a table. 
  // … 
   model.saveChanges(); 
 } 
  catch(operationException ex) 
 { 
  foreach(XmlaError err in ex.Results.OfType<XmlaError>().cast<XmlaError>()) 
  { 
   Console.WriteLine(“Error returned from the server:” + err.Messsage ); 
  } 
 } 
```

## <a name="next-steps"></a>Pasos siguientes

Otras excepciones relevantes son los siguientes:

- [Clase TomInternalException](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tominternalexception.aspx)
- [Clase TomValidationException](http://msdn.microsoft.com/library/microsoft.analysisservices.tabular.tomvalidationexception.aspx)
- [Clase JsonSerializationException](http://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_JsonSerializationException.htm)
